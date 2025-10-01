# Desafio de Implementação: Minha Primeira Stack com AWS CloudFormation
📚 Bootcamp Code Girls 2025: Santander & DIO
Este repositório documenta a aplicação prática de Infraestrutura como Código (IaC), utilizando o serviço AWS CloudFormation (CFN), conforme o desafio do bootcamp.

**1. Anotações de Aprendizado: O Que é o CloudFormation?**

- O AWS CloudFormation (CFN) é o serviço nativo da AWS para Infraestrutura como Código (IaC). Ele permite que você use arquivos de texto (chamados templates em YAML ou JSON) para descrever todos os recursos AWS que você quer provisionar.
- IaC vs. Manual: A principal vantagem é que o CFN garante que sua infraestrutura seja consistente e repetível. Em vez de clicar no console, você executa o código.
- Ciclo de Vida: O CFN gerencia todo o ciclo, desde a criação inicial até as atualizações e, fundamentalmente, a exclusão (desprovisionamento) dos recursos.
- Segurança: Reduz erros humanos e facilita a auditoria, pois toda mudança na infraestrutura está registrada no seu código-fonte.

**2. Principais Características do CFN**

- Templates: São os arquivos (YAML/JSON) que definem os recursos. São o "projeto" da sua infraestrutura.
- Recursos (Resources): A seção mais importante do template, onde você lista os serviços AWS a serem criados (ex: AWS::S3::Bucket, AWS::EC2::Instance).
- Rollback Automático: Um recurso de segurança essencial. Se um erro ocorrer durante o provisionamento, o CFN automaticamente deleta os recursos que foram criados com sucesso, voltando ao estado inicial.

**3. Conceito de Stack (Pilha)**

- Uma Stack é a unidade fundamental no CloudFormation.
- É o conjunto de todos os recursos criados pelo seu template.
- Em vez de gerenciar um Bucket S3, uma Função Lambda e uma Tabela DynamoDB separadamente, o CFN agrupa esses três como uma única Stack.
- Quando você deleta a Stack, você deleta todos os recursos que a compõem de uma só vez, garantindo a limpeza completa.

**4. Implementação do S3**

- O desafio consistiu em criar um Bucket S3 usando o CloudFormation, seguindo um fluxo simples e seguro:

**4.1. Template Utilizado**

- YAML

```AWSTemplateFormatVersion: '2010-09-09'
Description: "DESAFIO: AWS CloudFormation"
Resources:
  MeuBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: meu-bucket-teste-karollyne
```
**4.2. Processo Simplificado**

- Criação da Stack: Fiz o upload do template YAML no console do AWS CloudFormation.
- Configuração de Falha: Mantenha a opção "Reverter todos os recursos da pilha" ativa. (Isso é crucial!).
- Permissões: Deixei o campo Função do IAM vazio, permitindo que a Stack usasse as minhas permissões de usuário logado.
- Monitoramento: Acompanhei a aba Eventos até o status final CREATE_COMPLETE.
- Limpeza (Custo Zero): Imediatamente após a verificação, deletei a Stack. O CloudFormation desprovisionou o Bucket S3 e confirmou a limpeza com o status DELETE_COMPLETE.

**5. Insights e Conclusões**

- Rede de Segurança: O maior insight foi a importância da funcionalidade de Rollback. Ela atua como uma rede de segurança, garantindo que nenhum recurso indesejado ou incompleto permaneça na conta, o que é fundamental para evitar cobranças inesperadas.
- Gestão de Ambientes: Usar o CFN me ensinou que ambientes de nuvem devem ser tratados como código. Isso permite replicar, versionar e auditar a infraestrutura de maneira mais profissional.
- Exclusão Consciente: Em ambientes de aprendizado, a exclusão consciente da Stack é a última etapa do processo de IaC, garantindo que o ciclo de vida do recurso seja encerrado corretamente.

**6. Referências**

- [Documentação Oficial AWS CloudFormation](https://aws.amazon.com/pt/cloudformation/)
- [Referência de Recursos: AWS::S3::Bucket](https://docs.aws.amazon.com/pt_br/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket.html)
- Programa de Formação: Bootcamp Code Girls 2025
