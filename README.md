# Guarix – Emissor de Nota Fiscal (NF-e 55 e NFC-e 65)

> Este repositório é um **showcase** do projeto **Guarix**, um emissor de Nota Fiscal eletrônica modelos **55 (NF-e)** e **65 (NFC-e)**, focado em tornar a emissão de notas simples, rápida e segura para empreendedores e empresas.

---

## 🔗 Links

- 🌐 Versão web (produção): https://nfe.guarix.com.br/
- 🖥️ Versão desktop (NW.js): NÃO DISPONIVEL PARA DOWNLOAD
- 📱 App mobile: _se aplicável – adicione aqui o link da loja (https://play.google.com/store/apps/details?id=br.com.guarix.nfe)
- 📺 Vídeo demo no YouTube: _adicione aqui o link do vídeo de apresentação_

---

## 📌 Sobre este repositório

Este repositório **não contém o código-fonte** do Guarix.

Ele existe para:

- apresentar o produto de forma pública;
- servir como **portfólio técnico** do projeto;
- centralizar **prints, GIFs e vídeos** da aplicação em produção;
- documentar a solução em **alto nível** (arquitetura, principais decisões, desafios);
- descrever o **stack real** utilizado (Node.js, Vue 3, integrações fiscais etc.).

Se você está avaliando meu trabalho como desenvolvedor, aqui você encontra uma visão clara do que o sistema faz e de como ele foi estruturado.

---

## 🚀 Visão geral do produto

O Guarix é um emissor de Nota Fiscal Eletrônica que suporta:

- **NF-e – modelo 55** (venda de mercadorias);
- **NFC-e – modelo 65** (venda ao consumidor final).

A solução está disponível em:

- 🌐 **Versão Web** – acessível diretamente no navegador;
- 🖥️ **Versão Desktop** – construída com **NW.js**, para uso instalado em computadores (com opção de cache local de dados).

Pensado para negócios que precisam emitir notas diariamente sem depender de sistemas engessados ou processos manuais:

- interface amigável em **Vue 3**;
- fluxo guiado de emissão, com validações fiscais;
- automações para reduzir erros e rejeições da SEFAZ;
- disponibilidade tanto em ambiente web quanto desktop.

---

## 🌐 Web x Desktop (NW.js)

O Guarix foi projetado para funcionar em dois cenários complementares:

### Versão Web

- Acesso via navegador;
- Conexão ao banco de dados em **MySQL/MariaDB** no servidor;
- Ideal para uso multiusuário e acesso remoto.

### Versão Desktop (NW.js)

- Aplicação empacotada com **NW.js**, permitindo rodar como app de desktop;
- Utiliza **SQLite3** local para:
  - armazenar dados de forma mais próxima do usuário;
  - suportar cenários de conexão limitada ou intermitente (dependendo da configuração do projeto);
- Pode sincronizar com o backend/banco central em **MySQL/MariaDB**, conforme necessidade.

> Por isso o projeto utiliza **sqlite3** ou **MySQL/MariaDB**, caso seja multiplas maquinas ou somente uma com baixo recurso.

---

## 🧩 Principais funcionalidades

- ✅ Emissão de **NF-e (55)** e **NFC-e (65)**;
- ✅ **Suporte a múltiplos usuários**, com cada usuário podendo ter **1 ou N empresas** (multiempresa/multi-tenant);
- ✅ **Cadastro de produtos, clientes e orçamentos**;
- ✅ Configuração de **dados da empresa** e certificado digital;
- ✅ Sistema de **imposto automático (default)** para evitar dor de cabeça para usuários iniciantes  
  (configurações fiscais padrão por enquadramento, reduzindo erros em CFOP/CST/CSOSN etc.);
- ✅ Histórico de notas emitidas, com filtros por período, cliente, CFOP etc.;
- ✅ **Consulta de situação de NF-e/NFC-e** diretamente na SEFAZ;
- ✅ **Consulta automática de NF-e/NFC-e emitidas contra o CNPJ** do usuário (notas de terceiros);
- ✅ **Manifestos de destinatário (todos os tipos)** – ciência, confirmação, desconhecimento, operação não realizada;
- ✅ **Cancelamento de NF-e/NFC-e**, respeitando prazos e regras da legislação;
- ✅ **Relatório de XML emitidos** (consulta e exportação);
- ✅ Download de **XML** e visualização/impressão de **DANFE**;
- ✅ Envio de nota por e-mail ao cliente (XML + PDF);
- ✅ **Envio automático de XML mensalmente** para o responsável (ex.: contador ou e-mail cadastrado);
- ✅ Armazenamento em nuvem das notas autorizadas;
- ✅ **Sangria de caixa** (lançamentos de saída de caixa vinculados ao movimento de vendas);
- ✅ Relatórios básicos de faturamento (gráficos com Chart.js);
- ✅ **Relatório de faturamento e imposto esperado com base no enquadramento** – _em desenvolvimento_;

---

## 👥 Público-alvo

O Guarix é indicado para:

- MEIs;
- pequenas e médias empresas;
- prestadores de serviço;
- comércios de varejo que precisam emitir **NFC-e 65**;
- escritórios e profissionais que necessitam agilidade na emissão de NF-e.

---

## 🏗 Arquitetura em alto nível

Arquitetura simplificada da solução:

```mermaid
flowchart LR
    A1[Cliente Web<br/>Vue 3 no Browser] --> B[API / Backend Guarix<br/>Node.js + Express]
    A2[Cliente Desktop<br/>NW.js + Vue 3] --> B

    B --> C[(Banco de Dados Central<br/>MySQL/MariaDB)]
    B --> D[Serviços Fiscais<br/>SEFAZ – NF-e 55 / NFC-e 65]
    B --> E[Serviços de E-mail<br/>Nodemailer]
    B --> F[Armazenamento de Arquivos<br/>XML / PDFs DANFE]

    A2 --> G[(SQLite3 Local<br/>App Desktop)]
