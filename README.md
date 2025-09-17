# 🚀 Consolidando gerenciamento de instâncias EC2 na AWS.

## 1. **EC2 – Elastic Compute Cloud**
- É uma **máquina virtual na nuvem** da AWS.
- Modelo de serviço: **IaaS (Infrastructure as a Service)**.
*O que é responsabilidade do usuário?*
  - Instalar e configurar aplicativos.
  - Gerenciar dados.
  - Administrar conexões e acessos.

➡️ EC2 como **alugar um computador** onde você tem controle total sobre o sistema.

---

## 2. **Componentes de uma instância EC2**-
 **CPU, Memória, Rede** → o poder de processamento.
- **Disco (EBS)** → armazenamento de blocos.
- **Sistema Operacional (Linux/Windows)** → base para rodar apps.

---

## 3. **Escalabilidade**
- **Vertical:** aumentar recursos na mesma máquina (ex: mais CPU/RAM).
- **Horizontal:** aumentar o número de máquinas ou recursos (ex: mais instâncias EC2 ou mais discos).

➡️ Isso é chave para **otimizar custo** e não desperdiçar recursos.

---

## 4. **Armazenamento**### 
🔹 **EBS (Elastic Block Store)**- É como um **HD externo** que você conecta na sua instância EC2.
- Usado como disco raiz ou disco adicional.
- Permite **Snapshots** (cópias de segurança).

🔹 **S3 (Simple Storage Service)**
- Armazenamento de **objetos** (arquivos).
- Escalável, barato e confiável.
- Ideal para guardar backups, imagens, documentos e até arquivos de configuração.

---

## 5. **AMI (Amazon Machine Image)**
- Uma **imagem pré-configurada de sistema**.
- Pode ser pública (fornecida pela AWS) ou privada (criada por você).
- Serve para **replicar ambientes rapidamente**.
- Exemplo: você instala Apache + PHP em uma instância, cria uma AMI, e depois lança várias instâncias já configuradas.

---

## 6. **Snapshot (EBS Snapshot)**
- **Cópia de segurança** de um volume EBS.
- Guardada no S3 (internamente).
- Usos:
  - Backup de volumes.
  - Replicação de dados para outras regiões.
- Diferença para AMI:
  - **AMI** = backup do servidor inteiro (SO + dados + configuração).
  - **Snapshot** = backup apenas de um volume específico.

---

# 🏗️ Desafio de Arquitetura


### PIT STOP SHOP FLOW ###
Este projeto simula a arquitetura de uma **conveniência self-service**, utilizando serviços da AWS para gerenciar **estoque, vendas e relatórios automáticos**.  
A ideia é mostrar como aplicar os conceitos aprendidos de **EC2, EBS, S3 e Lambda** em um cenário prático 

## 🚀 Objetivo
- Controlar o estoque automaticamente conforme os clientes realizam compras.  
- Gerar relatórios diários com os produtos vendidos e aqueles que precisam ser repostos.  
- Enviar alertas automáticos (por e-mail ou SMS) quando o estoque de algum produto estiver baixo.

  
**Usuário → Instância EC2**
    - O cliente ou funcionário acessa o sistema da conveniência (ex.: registrar compras ou consultar estoque).
    - Esse sistema roda dentro da **instância EC2**, que funciona como o “cérebro” da aplicação.

**Instância EC2 → Volume EBS**
    - O **EBS** é como o “HD” do servidor.
    - É onde ficam os dados principais, como:
        - lista de produtos,
        - preços,
        - estoque atual,
        - transações de vendas.

**Instância EC2 → Bucket S3**
    - O EC2 também pode enviar arquivos e relatórios para o **S3**.
    - Exemplo: no fim do dia, o sistema gera um relatório de vendas em PDF ou CSV e o armazena no bucket S3.

**Volume EBS → Função Lambda**
    - A **Lambda** é chamada para **processar dados** sempre que necessário.
    - Exemplo:
        - Detecta no EBS que um produto chegou em quantidade mínima,
        - Executa uma função que dispara um alerta para a gerência ou até gera automaticamente um pedido de reposição.

**Bucket S3 → Relatórios**
    - O **S3** guarda os relatórios processados e organizados.
    - A gerência pode baixar relatórios de vendas, estoque baixo, produtos mais vendidos etc.

**📌 Ligando com a conveniência self-service**

- **Registrar vendas:** EC2 + EBS cuidam do cadastro dos produtos comprados e atualização do estoque.
- **Estoque:** EBS mantém os dados e a Lambda ajuda na automação (avisar sobre reposição).
- **Relatórios:** S3 armazena relatórios diários/semanais, que a Lambda pode processar automaticamente (ex.: gerar gráficos ou enviar por e-mail).

==================

### 🔹 Etapas do fluxo (estoque baixo + relatório)

**Cliente compra um produto**

- O usuário faz uma compra no self-service
- ação gera uma informação que vai para o sistema.

**EC2** 

- A compra é registrada no **EC2**, que é onde roda o sistema principal da loja.
- O EC2 atualiza os dados da venda: qual produto foi comprado, quantidade e valor.

**Armazenamento de dados (EBS)**

- Os dados da compra ficam armazenados no **banco de dados**.
- Isso garante que o estoque seja atualizado (se tinha 10, agora tem 9).

**S3 (armazenamento de arquivos)**

- O sistema salva informações no **S3**.

**Lambda (código por demanda)**

- Quando o S3 recebe um novo arquivo, ele dispara a **Lambda**.
- Essa função automática pode verificar se algum produto está acabando no estoque.

**Alerta (e-mail/SMS)**

- Se o estoque estiver baixo, a **Lambda** gera um alerta.
- Esse alerta pode ser enviado para o gerente da loja por e-mail, SMS ou até WhatsApp

📌 **Conclusão**

- **EC2 + EBS** → rodam o sistema e armazenam dados.
- **S3 + Lambda** → automatizam o processamento (alerta, relatórios).
- **Alerta** → resultado final que ajuda na tomada de decisão (ex.: repor estoque).




