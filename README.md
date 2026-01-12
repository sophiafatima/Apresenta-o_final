# 🍽️ FoodMatch - Sistema Inteligente de Receitas

Requisitos implementados 🛠:

☑ O sistema permite ao usuário se cadastrar no site.

☑ O usuário poderá redefinir a senha.

☑ O usuário deve poder inserir suas restrições alimentares e preferências.

☑ O sistema deve sugerir receitas personalizadas com base nos ingredientes disponíveis.

☑ O sistema deve ter uma interface intuitiva.

☑ O sistema deve oferecer suporte em português e inglês.

☑ O sistema deve ser acessível em dispositivos móveis e desktops.

☑ O sistema deve contar com um suporte ao usuário.

☑ O usuário poderá gerar uma lista de compras com os ingredientes das receitas.

☑ O sistema deve permitir que o usuário escolha entre modo claro e escuro.


## 📋 Sobre o Projeto

FoodMatch é uma plataforma web desenvolvida em Laravel que utiliza Inteligência Artificial para gerar receitas personalizadas baseadas nos ingredientes disponíveis do usuário. O sistema integra a API do Google Gemini para criar receitas únicas e adaptadas às preferências alimentares de cada usuário.

## 🚀 Funcionalidades Principais

### 🤖 Geração de Receitas com IA
- [ ] **Integração com Google Gemini AI**: Utiliza a API do Google Gemini para gerar receitas personalizadas
- [ ] **Sistema de Fallback Inteligente**: Caso a API falhe, utiliza um banco de receitas pré-programadas
- [ ] **Adaptação por Porções**: Calcula automaticamente ingredientes baseado no número de pessoas
- [ ] **Restrições Alimentares**: Suporte para vegano, vegetariano, sem lactose e sem glúten

### 👤 Sistema de Usuários
- [ ] **Cadastro e Login**: Sistema completo de autenticação
- [ ] **Perfil Personalizado**: Upload de foto, descrição e preferências alimentares
- [ ] **Gerenciamento de Sessão**: Controle de usuários logados
- [ ] **Reset de Senha**: Sistema de recuperação de senha

### 📱 Interface Responsiva
- [ ] **Design Moderno**: Interface limpa e intuitiva
- [ ] **Animações Personalizadas**: Animações exclusivas do FoodMatch
- [ ] **Menu Lateral Padronizado**: Navegação consistente em todas as páginas
- [ ] **Compatibilidade Mobile**: Totalmente responsivo

### 🛠️ Funcionalidades Técnicas
- [ ] **API RESTful**: Endpoints organizados para todas as funcionalidades
- [ ] **Banco de Dados SQLite**: Armazenamento eficiente de dados
- [ ] **Upload de Arquivos**: Sistema de upload de fotos de perfil
- [ ] **CORS Habilitado**: Suporte para requisições cross-origin

## Requisitos implementados 🛠️:

☑ O sistema permite ao usuário se cadastrar no site.

☑ O usuário poderá redefinir a senha.

☑ O usuário deve poder inserir suas restrições alimentares e preferências.

☑ O sistema deve sugerir receitas personalizadas com base nos ingredientes disponíveis.

☑ O sistema deve ter uma interface intuitiva.

☑ O sistema deve oferecer suporte em português e inglês.

☑ O sistema deve ser acessível em dispositivos móveis e desktops.

☑ O sistema deve contar com um suporte ao usuário.

☑ O usuário poderá gerar uma lista de compras com os ingredientes das receitas.

☑ O sistema deve permitir que o usuário escolha entre modo claro e escuro.


## 🏗️ Arquitetura do Sistema

### Backend (Laravel)
```
app/
├── Http/Controllers/
│   ├── ReceitaController.php     # Geração de receitas com IA
│   └── PublicidadeController.php # Gerenciamento de anúncios
├── Models/
│   ├── Usuario.php               # Modelo de usuário
│   └── Receita.php              # Modelo de receitas
└── database/
    └── migrations/              # Estrutura do banco de dados
```

### Frontend
```
public/
├── index.html                   # Página inicial
├── Login.html                   # Sistema de login
├── Cadastro.html               # Cadastro de usuários
├── Doof.html                   # Página principal (geração de receitas)
├── Perfil.html                 # Gerenciamento de perfil
├── suporte.html                # Sistema de suporte
└── assets/                     # CSS, JS e imagens
```

## 🔧 Como Funciona

### 1. Geração de Receitas com IA

**Fluxo Principal:**
```php
// ReceitaController.php
public function gerarReceita(Request $request)
{
    // 1. Recebe ingredientes e preferências
    $ingredientes = $request->get('ingredientes');
    $porcoes = $request->get('porcoes', 2);
    
    // 2. Tenta gerar com Gemini AI
    $receita = $this->chamarGeminiAPI($ingredientes, $porcoes);
    
    // 3. Se falhar, usa sistema inteligente local
    if (!$receita) {
        $receita = $this->gerarReceitaInteligente($ingredientes, $porcoes);
    }
    
    return response()->json(['success' => true, 'receita' => $receita]);
}
```

**Integração com Gemini AI:**
```php
private function chamarGeminiAPI($ingredientes, $porcoes, $preferencias)
{
    $prompt = "Crie uma receita usando: $ingredientes para $porcoes pessoas...";
    
    // Chamada HTTP para Google Gemini
    $response = curl_exec($ch);
    
    // Processa resposta JSON
    return json_decode($receitaText, true);
}
```

### 2. Sistema de Usuários

**Autenticação:**
```php
// Login
Route::post('/fazer-login', function (Request $request) {
    $user = Usuario::where('email_usuario', $request->email_usuario)->first();
    
    if (Hash::check($request->senha_usuario, $user->senha_usuario)) {
        session(['usuario_logado' => $user->nome_usuario]);
        return response()->json(['success' => true]);
    }
});
```

**Gerenciamento de Perfil:**
```php
// Upload de foto e dados
Route::post('/salvar-perfil', function(Request $request) {
    $usuario = Usuario::where('nome_usuario', session('usuario_logado'))->first();
    
    // Upload de foto
    if ($request->hasFile('foto_perfil')) {
        $file->move(public_path('storage/fotos'), $filename);
        $usuario->foto_perfil = 'fotos/' . $filename;
    }
    
    $usuario->save();
});
```

### 3. API Endpoints

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `GET/POST` | `/receita/gerar` | Gera receita com IA |
| `POST` | `/fazer-login` | Autenticação de usuário |
| `POST` | `/usuarios` | Cadastro de novo usuário |
| `GET` | `/perfil-dados` | Dados do perfil do usuário |
| `POST` | `/salvar-perfil` | Atualiza perfil do usuário |
| `POST` | `/upload-foto` | Upload de foto de perfil |
| `GET` | `/api/receitas` | Lista todas as receitas |

## 🛠️ Instalação e Configuração

### Pré-requisitos
- PHP 8.0+
- Composer
- Laravel 12.x
- SQLite

### Passos de Instalação

1. **Clone o repositório:**
```bash
git clone [url-do-repositorio]
cd food_match_novo
```

2. **Instale as dependências:**
```bash
composer install
```

3. **Configure o ambiente:**
```bash
cp .env.example .env
php artisan key:generate
```

4. **Configure a API do Gemini:**
```env
GEMINI_API_KEY=sua_chave_aqui
```

5. **Execute as migrações:**
```bash
php artisan migrate
```

6. **Inicie o servidor:**
```bash
php artisan serve --port=8001
```

## 🔑 Configuração da API Gemini

1. Acesse: https://makersuite.google.com/app/apikey
2. Crie uma nova chave de API
3. Adicione no arquivo `.env`:
```env
GEMINI_API_KEY=AIzaSy...
```

## 📊 Banco de Dados

### Tabelas Principais

**usuarios:**
- `id_usuario` (PK)
- `nome_usuario`
- `email_usuario`
- `senha_usuario`
- `foto_perfil`
- `descricao`
- `restricoes`

**receitas:**
- `id_receita` (PK)
- `nome_receita`
- `descricao_receita`
- `ingredientes`
- `preferencias`
- `restricao`

## 🎯 Funcionalidades Avançadas

### Sistema de Restrições Alimentares
O sistema detecta automaticamente restrições do usuário e adapta as receitas:
- [ ] **Vegano**: Remove todos os produtos de origem animal
- [ ] **Vegetariano**: Remove carnes mas mantém laticínios
- [ ] **Sem Lactose**: Substitui por alternativas sem lactose
- [ ] **Sem Glúten**: Utiliza farinhas alternativas

### Sistema de Fallback Inteligente
Caso a API do Gemini falhe, o sistema possui um banco de receitas pré-programadas:
- [ ] Mousse de Chocolate
- [ ] Lagosta Grelhada
- [ ] Escondidinho de Carne de Sol
- [ ] Frango à Parmegiana
- [ ] Sorvete de Manga
- [ ] E muitas outras...

### Cálculo Automático de Porções
- [ ] Todos os ingredientes são calculados automaticamente baseado no número de pessoas:
```php
($porcoes * 200) . 'g de chocolate meio amargo'
($porcoes * 3) . ' ovos'
```

## 🚀 Deploy

### Produção
1. Configure o servidor web (Apache/Nginx)
2. Aponte para a pasta `public/`
3. Configure as variáveis de ambiente
4. Execute `composer install --optimize-autoloader --no-dev`

## 🤝 Contribuição

1. Fork o projeto
2. Crie uma branch para sua feature
3. Commit suas mudanças
4. Push para a branch
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

## 👨💻 Desenvolvedor

Desenvolvido com ❤️ para revolucionar a forma como as pessoas cozinham!

---

**FoodMatch** - Transformando ingredientes em experiências culinárias únicas! 🍽️✨
