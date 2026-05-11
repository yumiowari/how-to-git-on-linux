# How to Git on Linux
Tutorial em Markdown de configuração básica do Git no Linux

## Sumário

1. [Instalar e configurar o Git Credential Manager](#passo-1)
2. [Gerar uma chave GPG](#passo-2)
    1. [(Opcional) Exportar e importar a chave GPG](#passo-opcional)
3. [Configurar o Git para utilizar a chave criada](#passo-3)
4. [Informar o nome e email para assinatura dos commits](#passo-4)
5. [Exportar a chave GPG para o GitHub](#passo-5)

## Passo 1
### Instalar e configurar o Git Credential Manager

- Baixe o pacote .deb: [gcm-linux-x64-x.x.x.deb](https://github.com/git-ecosystem/git-credential-manager/releases)
- Instale-o: `sudo apt install ./gcm-linux-x64-x.x.x.deb`
- Configure o GCM: `git-credential-manager configure`

## Passo 2
### Gerar uma chave GPG

- Execute: `gpg --full-generate-key`
    - Escolha tipo de chave RSA e RSA
    - Tamanho padrão (3072)
    - Válida indefinidamente (0)
    - Defina as informações pessoais (nome e email)
    - Insira uma senha segura
- Confira o identificador da chave gerada:
    - `gpg --list-secret-keys --keyid-format=long`
    - Copie o ID da chave após `sec    rsa3072/`

## Passo Opcional
### Exportar e importar a chave GPG

A chave GPG pode ser utilizada em mais de um computador.

Para isso, exporte a chave criada: `gpg --export-secret-keys --armor <gpg-key-id> > <gpg-key-id>.asc`

Salve o arquivo ASCII (.asc) em um backup externo.

Em outro computador, importe a chave:

`gpg --import ./<gpg-key-id>.asc`

Confira o nível de confiança máximo à chave:

- `gpg --edit-key <gpg-key-id>`
- `trust`
- `5`
- `quit`

## Passo 3
### Configurar o Git para utilizar a chave criada

- `git config --global credential.credentialStore gpg`
- `git config --global user.signingkey <gpg-key-id>`
- `git config --global commit.gpgsign true`
- `pass init <gpg-key-id>`

## Passo 4
### Informar o nome e email para assinatura dos commits

- `git config --global user.email "<email>"`
- `git config --global user.name "<username>"`

O nome de usuário e o email devem ser obrigatóriamente os mesmos do GitHub

## Passo 5
### Exportar a chave GPG para o GitHub

- `gpg --armor --export <gpg-key-id>`
- Copie o bloco de texto no terminal
- Desde `-----BEGIN PGP PUBLIC KEY BLOCK-----` até `-----END PGP PUBLIC KEY BLOCK-----`
- No perfil do GitHub > SSH and GPG keys
    - New GPG key
    - Informe um título
    - Cole o bloco de texto
 
`nano ~/.gitconfig` para visualizar as configurações.
