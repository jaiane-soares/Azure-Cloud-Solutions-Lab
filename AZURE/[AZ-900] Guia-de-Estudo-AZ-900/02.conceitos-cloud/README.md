
# Conceitos básicos de nuvem:

### O que é Cloud Computer?

Antigamente, as empresas sofriam com o alto custo e a complexidade de manter servidores físicos e infraestrutura local (On-premises). A computação em nuvem surge como a entrega de serviços de TI - como processamento, rede e armazenamento - via internet pagando pelo modelo de consumo pay as you go (pague conforme o uso). Isso permite que as empresas tenham alta disponibilidade e escalabilidade sob demanda. 


Por que as empresas precisam de Cloud Computer?

A nuvem mudou o jogo ao oferecer esses recursos via internet no modelo de "pague conforme o uso" (OpEx). É como parar de comprar geradores caros e passar a pagar apenas a conta de luz. Para quem quer rodar tecnologias de ponta, como Modelos de Linguagem (LLMs), a nuvem é o caminho mais rápido: você ganha um poder de processamento brutal sem precisar montar um datacenter gigante em casa.

>[!IMPORTANT]
> Entretanto, é preciso notar que a nuvem não é um cheque em branco. O alto custo de processamento para IA e as taxas de transferência de        dados têm impulsionado o movimento de Cloud Repatriation (repatriação de nuvem), onde empresas com demandas previsíveis e constantes   retornam ao On-premises para otimizar margens de lucro. A pergunta que fica: Empresas ainda precisam de Cloud? A resposta não é um "sim", nem um "não". A empresa deve pensar na nuvem para ter agilidade e inovação, mas precisa pensar em soberania de infraestrutura para uma demanda estável.

---

## Beneficios da nuvem:

### Alta Disponibilidade: (AH)

A Alta Disponibilidade é o beneficio da nuvem que garante a entrega de serviços sejam disponíveis quando necessário, ou quando houver alguma interferência.

#

### Escalabilidade:

A Escalabilidade é a capacidade da nuvem crescer ou diminuir conforme a demanda.


`dimensionamento vertical(escala vertical):`
Dimensionamento vertical é a capacidade de um recurso aumentar ou diminuir o processamento para se enquadrar no que o cliente deseja. Ex: aumentar a RAM

`dimensionamento horizontal(escala horizontal):`
Dimensionamento horizontal é a capacidade de reduzir ou aumentar unidades de recurso conforme o necessário. Ex: adicionar VMs

>[!IMPORTANT]
>Exemplo de cenário: Tenho uma pizzaria, o forno é bem fraco e não vai dar para aguentar muito tempo. Eu compro um forno mais potente: escala vertical.
>
>Exemplo de cenário: Sou o Naruto, mas sozinho não consigo matar o oponente, então faço clones da sombras: escala horizontal.
`(no caso da pizza isso seria comprar varios fornos iguais com a mesma capacidade)`


## descrever os tipos de serviço em nuvem:

### IaaS - Infrastructor as a service (infraestrutura como serviço):

O provedor entrega recursos de computação virtualizados (Compute, Storage, Networking) via um Hipervisor.

`Responsabilidade:` O cliente é dono da stack de software completa. Isso inclui a escolha e o patching do SO, a instalação do Runtime (ex: instalar o JDK 21 para o Java) e toda a configuração de rede interna.

`Resumo:` O cliente gerencia a VM.

#

### PaaS - Plataform as a Service (plataforma como serviço):

O provedor abstrai o SO e o Runtime. Ele te entrega um ambiente de execução pronto.

`Responsabilidade: O cliente é responsável apenas pelo Código da aplicação e pelos dados.`

`Resumo:` Você desenvolvendo seu código. Azure Apps Service.

#

### SaaS - Software as a Service (Software como serviço):

Entrega de uma aplicação completa via web. Toda a stack (Infra, SO, Runtime, código e banco de Dados) é gerenciada pelo provedor.

`Responsabilidade:` O cliente gerencia apenas o acesso (Identidade) e as configurações de usuário. O cliente consome a API ou a interface, mas não mexe em uma linha de código do servidor.

`Resumo:` você usando o Microsoft 365.

# Modelo de responsabilidade compartilhada (Cloud Computing)

<div align="center">
  
| Camada de tecnologia | IaaS (Infraestrutura) | PaaS (Plataforma) | SaaS (Software) |
| :--- | :--- | :--- | :--- |
| **Aplicação** | Cliente | Cliente | Provedor |
| **Dados** | Cliente | Cliente | Cliente/Provedor |
| **Runtime (Ex: Java/JRE)** | Cliente | Provedor | Provedor |
| **Middleware** | Cliente | Provedor | Provedor |
| **Sistema Operacional** | Cliente | Provedor | Provedor |
| **Virtualização (Hypervisor)** | Provedor | Provedor | Provedor |
| **Hardware (Servidor/Rede)** | Provedor | Provedor | Provedor |
</div>

---

## Imagem extraida do site da Microsoft Learn: 

![imagem](https://github.com/JaiDev-bot/Azure-Cloud-Solutions-Lab/blob/main/AZURE/%5BAZ-900%5D%20Guia-de-Estudo-AZ-900/02.conceitos-cloud/responsabilidades.png)

--

## Infraestrutura de nuvem

### Regiões e Pares de Região (Region Pairs)
   
`A real: Se um furacão, terremoto ou um estagiário atormentado derrubar uma região inteira, a outra segura o tranco. O Azure atualiza uma região por vez em cada par para garantir que você não fique offline. Se você não configurar o failover pro par, seu SLA é uma piada.`

Na teoria, é lindo. Na prática, é o seu seguro de vida.

Uma Região é um conjunto de datacenters próximos. O Par de Região é uma região irmã localizada a pelo menos 300 milhas (480 km) de distância.

### Zonas de Disponibilidade (Availability Zones - AZ)
Dentro de uma região, você tem as AZs. São datacenters isolados fisicamente, com energia, resfriamento e rede independentes.

`A real: É redundância dentro da redundância. Se o datacenter A pegar fogo, o B e o C continuam rodando. Se sua aplicação não for zone-redundant, você está contando com a sorte. E engenheiro que se preze não conta com sorte.`

### Conjuntos de Disponibilidade (Availability Sets)
Aqui a gente desce pro nível do rack. Serve para proteger contra falhas de hardware local.

Domínios de Atualização (UD): Quando a Microsoft decide atualizar o host, ela não reinicia tudo de uma vez. Ela faz por grupos.

Domínios de Falha (FD): Separa suas VMs em racks diferentes com fontes de energia e switches diferentes.

`A real: É para evitar que um cabo de rede mal encaixado ou uma atualização de segurança transforme seu serviço em um erro 404.`

### Recuperação de Desastres (DR)
O círculo no topo do desenho. É o plano de "deu merda geral".

`A real: Não é só ter backup. É ter um RTO (Recovery Time Objective) e um RPO (Recovery Point Objective) definidos. Se você demora 10 horas para subir o sistema de novo, sua empresa já perdeu milhões e você provavelmente seu emprego.`

![imagem](https://github.com/JaiDev-bot/Azure-Cloud-Solutions-Lab/blob/main/AZURE/%5BAZ-900%5D%20Guia-de-Estudo-AZ-900/02.conceitos-cloud/Regioes-2026-01-24-1416.png)




---
[⬅️ Anterior](../01.guia-estudo/README.md) | [🏠 Home](../../../README.md) | [Próximo: 03. Azure Services ➡️](../03.Azure-services/README.md)




