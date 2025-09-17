# Anotações do curso AWS

- EC2: máquinas virtuais na AWS
- EBS: armazenamento em blocos
- S3: armazenamento de objetos
- Lambda: funções serverless

**#comandos Git Bash:**
- ls = para confirmar em qual pasta está e quais os documentos dentro da mesma
- cd = mudar de diretória (mas a melhor opção é ir diretamente na pasta executar comando

**INSTÂNCIAS EC2**

**EC2** - Elastic Compute Cloud, são as máquinas virtuais na AWS, podendo ser com sistema operacional Windows ou Linux.

No modelo Cloud, **uma EC2 é do tipo IAAS** ou seja, quando criamos um EC2 estamos utilizando o tipo de infraestrutura como serviço;

**E qual seria nossa responsabilidade sobre este recurso?** - Seria dos aplicativos, dados e conexões que fazemos

**Uma EC2 é composta por:**

- CPU
- Rede
- Memória
- Sistema
- Disco
- Sistema Operacional

**EC2 - TERMINOLOGIA**

- Amazon Elastic Compute Cloud (EC2) nos fornece a capacidade de computação na cloud da AWS

**OS TIPOS DE INSTÂNCIA EC**

**Instância** é uma máquina virtual dentro da AWS

[calculator.aws/#/](http://calculator.aws/#/) - para saber o custo estimado da instância desejada para a sua demanda/necessidade.

- quando falamos em otimização de recursos, estamos apontando para o “custo”, ou seja, otimizar recurso é poupar custos na AWS

Escalar verticalmente - significa acrescentar ou reduzir capacidade de um recurso em um mesmo nó.

Escalando Horizontalmente - quando vc aumenta o número de recursos, Por exemplo, adicionando mais um disco rígido, adicionando mais uma instância.

**ARMAZENAMENTO NA NUVEM - - EBS**

Amazon EBS - Elastic Block Store (EBS) - storage altamente confiàvel que pode ser anexado em qualquer instância EC2. com o EBS a capacidade de expansão se torna mais rápida, com apenas alguns clicks.

EBS -  seria como anexar um HD externo.

**ARMAZENAMENTO NA NUVEM - S3**

Amazon S3 - Amazon Simple Storage Service - serviço de armazenamento de objetos em nuvem oferecidos pela AWS

CRIAÇÃO E USO DE IMAGENS AMI (Amazon Machine Image)

Imagem de uma máquina virtual criada 

- no amazon  EC2 uma AMI é uma imagem de máquina virtual prè-configurada, ao qual a partir disto, pode ser criada outras instâncias.

Principais pontos:

- **AMI  podem ser criadas** a partir de instâncias em execução ou paradas. Isto lhe permite capturar um intantâneo de seu ambiente configurado;
- **AMIs públicas e privadas:** há possibilidade da utilização de já existentes (píblicas) ou a criar sua própria (privada) afim da personalização e segurança disponível.
- **Personalização:** possibilidade de personalizar uma instâcia (instalar software, configurar definições) e podendo ser criada uma AMI a partir disto, ao qual, isto facilita a replicação do seu ambiente.
- **Iniciar Instâncias:** Para executar instâncias no EC2, é selecionado uma AMI, assim fornencendo as informações necessárias para iniciar uma instância, como o volume do dispositivo raiz e as permissões de inicialização.
- **Tipos de AMI:** Amazon Linux, Windows e outros, são exemplos de quais podem escolher baseado nos requisitos da aplicação e do sistema.

**SNAPSHOT - EBS**

- muito utilizado para fazer back-ups de ambientes ou fazer uma réplica para outras regiões
- insfraestrutura = a ver com o disco de servidor virtual
- EBS - IAAS
- Snapshot do EBS é possível configurar a frequência com que os snashots são tirados, nrnalmente é feito back up de ambientes produtivos;
- diferença entre AMI e Snapshot:

AMI = na amazon EC2 é feito o back up de um servidor inteiro, incluindo volumes EBS anexados;

SNAPSHOT = cópia manual de um determinado volume, armazenadas do S3;
