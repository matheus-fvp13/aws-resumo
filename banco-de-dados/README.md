# Armazenamento e banco de dados na AWS

## Armazenamento de dados em nuvem
### Tipos de armazenamento
Um tipo de armazenamento define como um dado será persistido.
- **Armazenamento de Objetos**:
    - Object Storage.
    - Dados como objetos (arquivos e metadados)
    - Dados não estruturados
    - Casos de uso: Data lakes, Mídias, Backup e recuperação.
- **Armazenamento de Arquivos**:
    - File Storage.
    - Sistema de arquivos compartilhados.
    - Permite acesso por meio de servidores, aplicações e usuários.
    - Análogia com pastas compartilhadas em uma rede.
    - Casos de uso: Ferramentas de desenvolvimento, diretórios pessoais.
- **Armazenamento de Blocos**:
    - Block Storage.
    - Armazenamento de blocos: HDD, SSD.
    - Dispositivos com diferentes configurações de leitura e escrita.
    - Casos de uso: Máquinas virtuais, conteiners, banco de dados.
## Amazon Elastic Block Store - EBS
Quando usamos uma instância EC2 para rodar algum serviço não alocamos um espaço fisico dedicado para 
armazenamento de dados. As instâncias podem ser executadas em computadores diferentes em determinados
momentos, logo depender da memória secundaria (HD ou SSD) do host para persistir nossos dados não é o ideal. 
### Volume Instance Store
- Armazenamento de Blocos
- Discos anexados fisicamente ao computador host.
- Ideal para dados de armazenamento temporário como buffers, caches, dados de rascunho.
- Dados serão **perdidos** se:
    - Falha de disco de uma unidade
    - Instância parada.
    - Instância hibernada.
    - Instância encerrada.

O **EBS** permite anexar um volume físico dedicado a uma instância EC2, suas principais caracteristicas
são:
- Armazenamento em blocos.
- Block, blocos = HD, físico.
- Projetado para Amazon Elastic Compute Cloud (EC2).
- HDs são chamados "volumes".
### Como o EBS funciona?
Ao utilizar o EBS seus dados não serão perdidos.
1. Defina o tipo de volume (HDD-based ou SSD-based).
    - **HDD**: Mais lento, mais barato, pode ser dividido em **disco rígido frio** e **otimizado para throughput**. 
    - **SSD**: Mais rápido, mais caro, pode ser dividido em **volumes SSD de uso geral** e **IOPS provisionados**.
2. Escolha tamanho e configurações.
3. Anexe o volume a uma instância EC2.
### E os Backups?
Podemos usar **Snapshots** e **Backup incremental**
- No primeiro dia tudo o que estiver no HD serão copiados.
- No segundo dia apenas os dados alterados é que serão copiados.
- ....
- O historico de alterações permite que o volume possa ser recriado.

