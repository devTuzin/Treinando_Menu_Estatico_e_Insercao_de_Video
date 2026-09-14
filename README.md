# 🎬 CorporateFlix — Portal de Treinamentos Internos

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen?style=for-the-badge)

MVP de alta performance desenvolvido para uma startup de EdTech. A plataforma foi construída com foco em **rigoroso controle de banda**, **roteamento estático sem rechargem de página** e **isolamento estrito de escopos CSS**.

---

## 📌 Sumário
- [Sobre o Projeto](#-sobre-o-projeto)
- [Arquitetura & Requisitos Técnicos](#-arquitetura--requisitos-técnicos)
- [Engenharia de Mídia](#-engenharia-de-mídia)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [Como Executar](#-como-executar)

---

## 🚀 Sobre o Projeto

O **CorporateFlix** responde às limitações de infraestrutura de servidores com alto tráfego. A interface entrega uma experiência fluida estilo streaming (Single Page Application via encapsulamento), garantindo a otimização no consumo de dados de vídeos e a eliminação de *bugs* visuais de layout.

---

## 🏗️ Arquitetura & Requisitos Técnicos

* **Roteamento Sem Refresh:** Uso de menu estático conectado a um `<iframe>` dinâmico via atributo `target="painel-conteudo"`. As subpáginas são atualizadas sem recarregar o documento principal (`index.html`).
* **Modularidade de Estilos (CSS Isolado):** Divisão estrita em arquivos independentes para evitar contaminação de escopo (*CSS leak*):
  * `shell.css`: Bloqueia a rolagem geral da aplicação (`overflow: hidden`).
  * `conteudo.css`: Habilita a rolagem vertical (`overflow-y: auto`) apenas no contêiner interno das subpáginas.
* **Prevenção de Bugs Visuais:** 
  * Remoção de bordas 3D/afundadas no painel (`border: none`).
  * Eliminação de barras de rolagem duplas e espaços fantasmas inline (`display: block`).

---

## 🎥 Engenharia de Mídia

### 📹 Subpágina 1: Módulo de Aula Padrão (`aula-padrao.html`)
* **Otimização de Banda:** Configurado com `preload="metadata"`. O download do arquivo pesado de vídeo fica estritamente bloqueado até a ação explícita de *play* do usuário.
* **Prevenção de Layout Shift:** O navegador lê apenas os metadados iniciais para reservar o espaço exato na tela (evitando pulos no layout).
* **Fullscreen Liberado:** Concessão explícita no `<iframe>` principal via atributos `allow="fullscreen"` e `allowfullscreen`.

### 📺 Subpágina 2: Tela de Boas-Vindas (`boas-vindas.html`)
* **Vídeo Ambiente (Autoplay Bypass):** Configurado com `autoplay`, `muted`, `loop` e `playsinline`. O silenciamento forçado cumpre as políticas de segurança dos navegadores para liberar a reprodução automática contínua.
* **Interface Limpa:** Ausência do atributo `controls` para atuar puramente como fundo visual estético.

---

## 📁 Estrutura do Projeto

```text
corporateflix/
├── index.html            # Shell principal (menu estático e painel)
├── boas-vindas.html      # Subpágina 2 (vídeo ambiente)
├── aula-padrao.html      # Subpágina 1 (aula com foco em performance)
├── shell.css             # Estilos do container e layout global
├── conteudo.css          # Estilos internos das subpáginas
└── assets/               # Mídias locais (vídeos e imagens)
