# Void Linux – Zen Kernel (Custom Build para Void Linux glibc x86_64)

Kernel Zen compilado manualmente para **Void Linux**, disponibilizado via **GitHub Releases**.

Este repositório **não** contém binários no histórico Git. Os pacotes `.xbps` são distribuídos apenas nas *Releases*.

---

## Pacotes disponíveis

Release atual: **v6.18.7-zen**

* `linux6.18-zen-6.18.7_1.x86_64.xbps`
* `linux6.18-zen-headers-6.18.7_1.x86_64.xbps`

Inclui:

* Kernel Zen
* Headers correspondentes

Release: https://github.com/erickdevit/void-zen-kernel/releases/download/v6.18.7-zen/

---

## Verificação de integridade (recomendado)

### 1. Baixar arquivos

Baixe os arquivos diretamente da release:

* Pacotes `.xbps`
* `SHA256SUMS`
* `SHA256SUMS.asc`

---

### 2. Importar chave GPG

```bash
gpg --keyserver hkps://keys.openpgp.org --recv-keys 7C821F19D1835CF828AD4653AE0D1BC5DAE9356A
```

---

### 3. Verificar assinatura

```bash
gpg --verify SHA256SUMS.asc SHA256SUMS
```

Deve retornar **assinatura válida**.

---

### 4. Verificar checksum

```bash
sha256sum -c SHA256SUMS
```

Todos os arquivos devem retornar `OK`.

---

## Instalação no Void Linux

### Opção A — Instalação manual (arquivo local)

No diretório onde estão os pacotes:

```bash
sudo xbps-install --repository=./ linux6.18-zen linux6.18-zen-headers
```

Após a instalação:

```bash
sudo update-grub
reboot
```

---

### Opção B — Usar como repositório remoto (via URL)

É possível adicionar este kernel como um **repositório xbps remoto**, permitindo instalação via URL.

>  Observação: este método **não oferece atualizações automáticas** como um repositório oficial, mas facilita a instalação sem download manual.

#### 1. Criar arquivo de repositório

```bash
sudo tee /etc/xbps.d/99-zen-kernel.conf << 'EOF'
repository=https://github.com/erickdevit/void-zen-kernel/releases/download/v6.18.7-zen/
EOF
```

#### 2. Atualizar índice e instalar

```bash
sudo xbps-install -S
sudo xbps-install linux6.18-zen linux6.18-zen-headers
```

Após a instalação:

```bash
sudo update-grub
reboot
```

---

---

## Receita de build (Void Packages)

Este repositório **inclui a receita completa** do pacote para o sistema de build do Void Linux (`xbps-src`).

Local:

```
srcpkgs/linux6.18-zen/
├── template
├── files/
└── patches/
```

Isso permite que qualquer pessoa:

* audite como o kernel foi compilado
* reproduza o build localmente
* adapte flags, patches ou versão

---

### Como buildar localmente

Pré-requisitos:

* Void Linux
* Repositório `void-packages` configurado

Passos:

```bash
git clone https://github.com/void-linux/void-packages.git
cd void-packages
```

Copie a receita deste repositório:

```bash
cp -r CAMINHO_DESTE_REPO/linux6.18-zen srcpkgs/
```

Build:

```bash
./xbps-src pkg linux6.18-zen
```

Os pacotes finais serão gerados em:

```
hostdir/binpkgs/
```

---

## Autor

**erickdevit**
Unidos pelo Tux 🐧

---

## Build e uso

Este passo existe para garantir que todas as dependências estejam corretamente resolvidas antes da execução, evitando erros em tempo de execução.

Se você estiver usando uma *recipe*, certifique-se de seguir a ordem descrita, pois ela prepara o ambiente, configura permissões e valida caminhos necessários.
