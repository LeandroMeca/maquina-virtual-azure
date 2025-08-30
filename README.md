<h1>Documentação Técnica: Criação de Máquina Virtual no Microsoft Azure</h1>

<p><strong>Versão:</strong> 1.0</p>
<p><strong>Data:</strong> 29/08/2025</p>
<p><strong>Autor:</strong> [Nome do Autor/Equipe]</p>

<h2>1. Introdução</h2>
<p>
Este documento estabelece o procedimento padrão para a criação de Máquinas Virtuais (VMs) na plataforma Microsoft Azure. O objetivo é detalhar as etapas cruciais do processo, com ênfase nas configurações de disponibilidade, armazenamento e no impacto dessas escolhas sobre o Acordo de Nível de Serviço (SLA - Service Level Agreement) do recurso provisionado.
</p>

<h2>2. Acesso ao Serviço de Máquinas Virtuais</h2>
<p>
Para iniciar o processo de criação de uma VM, o serviço pode ser localizado no portal Azure através de duas abordagens principais:
</p>
<p>

<strong>Utilizando a Barra de Pesquisa:</strong> A forma mais direta é digitar "Máquinas Virtuais" na barra de pesquisa global localizada no topo do portal.
</p>
<p>

<strong>Navegando pelo Menu de Serviços:</strong>
<ul>
<li>Clique no ícone de menu (três linhas horizontais) no canto superior esquerdo.</li>
<li>Selecione a opção "Todos os serviços".</li>
<li>Na categoria "Computação", localize e clique em "Máquinas Virtuais".</li>
</ul>
</p>

<h2>3. Configuração da Máquina Virtual</h2>
<p>
Na tela de "Máquinas Virtuais", clique em "+ Criar" para iniciar o assistente de configuração. As seções a seguir detalham os parâmetros mais críticos.
</p>

<h3>3.1. Detalhes Fundamentais (Aba "Básicos")</h3>
<p>
<strong>Nome da Máquina Virtual:</strong> Defina um nome único que siga as convenções de nomenclatura da organização.
</p>
<p>
<strong>Região:</strong> Selecione o datacenter ou conjunto de datacenters onde a VM será hospedada. A escolha da região afeta a latência para os usuários finais e a conformidade com as políticas de soberania de dados.
</p>
<p>
<strong>Opções de Disponibilidade:</strong> Esta é uma configuração crítica para determinar a resiliência da VM contra falhas.
<ul>
<li><strong>Zona de Disponibilidade:</strong> Oferece o mais alto nível de proteção ao distribuir VMs em datacenters fisicamente separados dentro da mesma região. Se um datacenter (zona) falhar, as VMs nas outras zonas permanecem operacionais. A utilização de Zonas de Disponibilidade aumenta o tempo de atividade garantido (SLA).</li>
<li><strong>Conjunto de Disponibilidade:</strong> Protege contra falhas de hardware dentro de um único datacenter, distribuindo as VMs em diferentes racks (domínios de falha) e hosts de manutenção (domínios de atualização).</li>
<li><strong>Nenhuma redundância de infraestrutura:</strong> Opção adequada para ambientes de desenvolvimento ou teste, onde a alta disponibilidade não é um requisito.</li>
</ul>
</p>

<h3>3.2. Armazenamento e Contas de Armazenamento</h3>
<p>
Os discos da VM são armazenados em Contas de Armazenamento (Storage Accounts) do Azure. A configuração de redundância dessas contas é vital para a durabilidade dos dados. As Contas de Armazenamento podem ser gerenciadas separadamente em "Todos os serviços" -> "Contas de Armazenamento". Ao criar uma, as seguintes opções de redundância estão disponíveis:
<ul>
<li><strong>LRS (Armazenamento com Redundância Local):</strong> Mantém três cópias dos dados dentro de um único datacenter.</li>
<li><strong>ZRS (Armazenamento com Redundância de Zona):</strong> Replica os dados de forma síncrona em três Zonas de Disponibilidade diferentes dentro da mesma região.</li>
<li><strong>GRS (Armazenamento com Redundância Geográfica):</strong> Replica os dados para uma região secundária a centenas de quilômetros de distância.</li>
</ul>
</p>

<h2>4. O Acordo de Nível de Serviço (SLA)</h2>
<p>
O SLA é a garantia de tempo de atividade que a Microsoft oferece para um serviço. É fundamental entender que o SLA não é um valor fixo; ele é diretamente determinado pela arquitetura escolhida durante a criação do recurso. A solicitação de um SLA específico é, portanto, uma requisição implícita do usuário ao projetar a solução.
</p>

<h3>4.1. Previsão de Tempo de Inatividade</h3>
<p>
Saber o modelo de serviço contratado é essencial para prever o tempo máximo de inatividade aceitável. O SLA para VMs do Azure varia significativamente:
<ul>
<li><strong>VM Única com Discos Premium SSD/Ultra Disk:</strong> Garante um SLA de 99.9%.</li>
<li><strong>VMs em um Conjunto de Disponibilidade:</strong> A utilização de duas ou mais VMs em um Conjunto de Disponibilidade eleva o SLA para 99.95%.</li>
<li><strong>VMs em Zonas de Disponibilidade:</strong> A distribuição de duas ou mais VMs em Zonas de Disponibilidade distintas oferece o SLA mais alto, de 99.99%.</li>
</ul>
</p>
<p>
<strong>Exemplo de Tempo de Inatividade Máximo por Mês:</strong>
<ul>
<li>SLA 99.9%: ~43.8 minutos</li>
<li>SLA 99.95%: ~21.9 minutos</li>
<li>SLA 99.99%: ~4.4 minutos</li>
</ul>
</p>

<h2>5. Conclusão</h2>
<p>
Ao provisionar uma Máquina Virtual no Azure, as decisões de arquitetura relativas à disponibilidade (Zonas ou Conjuntos de Disponibilidade) e à redundância de armazenamento são tão importantes quanto a seleção de CPU e memória. Não podemos esquecer que o SLA é uma consequência direta dessas escolhas. Para garantir que os objetivos de negócio sejam atendidos, é imperativo analisar os requisitos de tempo de atividade antes da implantação, a fim de contratar o modelo de serviço adequado e ter uma previsão clara do tempo de inatividade potencial do serviço.
</p>
