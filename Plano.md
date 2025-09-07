# sgppc

Plano de Projeto: Sistema de Gestão de Processos de Produtos Controlados (SGPPC)
1. Resumo Executivo
Contexto: Setor de Fiscalização de Produtos Controlados do Exército, ano de 2019. A gestão de processos é manual e ineficiente, gerando lentidão na análise e dificuldade na localização de documentos físicos.

Objetivo: Desenvolver e implementar um sistema de gestão digital para modernizar o processo, reduzir a demanda física e otimizar o fluxo de trabalho interno e externo.

Tecnologias-Chave: Java (com Spring Boot e JavaFX), MySQL/PostgreSQL.

Metas de Negócio:

Redução de 80% na manipulação de documentos físicos.

Diminuição de 50% no tempo médio de análise de processos.

Melhora da experiência do usuário externo (despachantes) através de agendamento online.

2. Visão Geral do Projeto
O SGPPC é um sistema modular, dividido em três partes principais que interagem entre si, mas podem ser desenvolvidas de forma independente (seguindo uma metodologia ágil, como Scrum ou Kanban).

Módulo 1 (Digitalização): Aplicação desktop para uso interno, focada na importação de documentos físicos existentes para o formato digital.

Módulo 2 (Gestão Digital): Extensão do Módulo 1, para gerenciar novos processos que já chegam digitalmente, incluindo funcionalidades de busca e visualização.

Módulo 3 (Agendamento Online): Plataforma web para o público externo (despachantes), permitindo o agendamento de horários para atendimento.

3. Fases do Projeto e Cronograma (Simulado)
Este cronograma é uma estimativa. A duração de cada sprint pode variar.

Fase 1: Iniciação e Planejamento (1 Semana)

Definição de requisitos e escopo.

Escolha da arquitetura e das tecnologias.

Criação do banco de dados e da estrutura inicial do projeto.

Fase 2: Desenvolvimento da Sprint 1 (2-3 Semanas)

Foco no Módulo 1: Digitalização.

Fase 3: Desenvolvimento da Sprint 2 (2-3 Semanas)

Foco no Módulo 2: Gestão Digital (busca e visualização).

Fase 4: Desenvolvimento da Sprint 3 (3-4 Semanas)

Foco no Módulo 3: Agendamento Online.

Fase 5: Testes e Implantação (1-2 Semanas)

Realização de testes de aceitação e integração.

Implantação em um ambiente de produção simulado.

Elaboração da documentação técnica e do usuário.

4. Guia de Desenvolvimento Detalhado: Sprint 1 (Módulo de Digitalização)
Este é o nosso roteiro de implementação.

4.1. Configuração do Ambiente e Projeto
Ferramentas: Instalar JDK 11 e configurar o ambiente em uma IDE (IntelliJ IDEA ou Eclipse).

Projeto Maven: Criar um projeto Maven com as dependências necessárias no arquivo pom.xml:

javafx-controls e javafx-fxml

mysql-connector-java ou postgresql

twain4java (simulação)

commons-io (para manipulação de arquivos)

log4j ou slf4j

Configuração do Banco de Dados: Executar o script SQL para criar o banco de dados sgppc e a tabela processo.

SQL

CREATE DATABASE IF NOT EXISTS sgppc;
USE sgppc;

CREATE TABLE IF NOT EXISTS processo (
    id INT AUTO_INCREMENT PRIMARY KEY,
    numero_processo VARCHAR(50) NOT NULL UNIQUE,
    nome_requerente VARCHAR(255) NOT NULL,
    data_entrada DATE NOT NULL,
    path_digital VARCHAR(255) NOT NULL,
    localizacao_fisica VARCHAR(100),
    status ENUM('Em Análise', 'Finalizado', 'Arquivado') NOT NULL,
    observacoes TEXT,
    data_digitalizacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
4.2. Estrutura do Código e Camadas
Pacotes:

br.com.exercito.sgppc.model

br.com.exercito.sgppc.dao

br.com.exercito.sgppc.service

br.com.exercito.sgppc.controller

br.com.exercito.sgppc.app

Classes Essenciais:

Processo.java (Model): Classe POJO com os atributos da tabela processo.

Conexao.java (Utils): Classe para gerenciar a conexão com o banco de dados via JDBC.

ProcessoDAO.java (DAO): Implementa os métodos salvarProcesso() e existeProcesso().

4.3. Lógica de Negócio e Manipulação de Arquivos
ProcessoService.java (Service):

Implementar o método digitalizar(Processo processo, File arquivo) que:

Verifica a existência do processo no banco de dados.

Cria uma estrutura de pastas lógica (/arquivos_digitais/ano/mes/).

Copia o arquivo para o diretório correto.

Salva o path_digital no objeto processo.

Chama o ProcessoDAO para salvar os dados no banco.

4.4. Interface Gráfica (JavaFX)
digitalizacao.fxml:

Criar o layout com campos de entrada para os metadados do processo e um botão "Digitalizar".

DigitalizacaoController.java (Controller):

Conectar os elementos do FXML aos métodos do ProcessoService.

Implementar a lógica para coletar dados da interface, chamar o serviço e exibir mensagens de sucesso ou erro ao usuário.

5. Próximos Passos
Após a conclusão e validação da Sprint 1, passaremos para a Sprint 2, que focará na implementação da busca e visualização de arquivos. Em seguida, a Sprint 3 irá focar no agendamento online.
