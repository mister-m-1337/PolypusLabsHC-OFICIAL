# Listagem de diretório sem autenticação

**PolypusLabsHC · Nota técnica anonimizada**

## Classificação

| Campo | Resultado |
|---|---|
| Estado | Confirmado na coleta histórica |
| Severidade | Média, preliminar |
| Categoria | Exposição de informações por listagem de diretório |
| CVSS | Não atribuído |

## Achado confirmado

Uma requisição HTTP GET sem credenciais retornou status 200 e uma página de listagem de diretório. O HTML apresentava links para arquivos e subdiretórios da aplicação, acompanhados de metadados de tamanho e data.

A listagem revelou nomes de arquivos de configuração, manifesto de dependências, componentes de inicialização, log de instalação e diretórios de implantação. Esses elementos foram identificados na página de índice; isso não comprova que o conteúdo dos arquivos pudesse ser baixado.

## Impacto observado

A exposição permite reconhecer a organização da aplicação e descobrir caminhos internos de implantação sem autenticação. Essas informações podem orientar reconhecimento adicional e tentativas de acesso a artefatos conhecidos.

O vazamento de configurações, dependências detalhadas, segredos ou conteúdo de logs dependeria de leitura efetiva dos arquivos. Essa leitura não foi confirmada no material analisado.

## Limites da evidência

- O achado confirmado é a exposição da listagem e de seus metadados.
- Não foram demonstrados download de arquivos sensíveis, acesso arbitrário ao sistema de arquivos, escrita, execução remota ou acesso ao banco de dados.
- Cabeçalhos de identificação de tecnologia não comprovam versão real, atualização instalada ou aplicabilidade de uma CVE.
- Uma resposta em HTTP não comprova ausência de HTTPS em outro endereço ou porta.
- Hipóteses de CVEs e falhas de conectividade não foram convertidas em vulnerabilidades confirmadas.
- Esta publicação descreve uma observação histórica. O estado atual e eventual correção não foram revalidados.

## Correção recomendada

1. Desativar a listagem de diretório no escopo da aplicação e do servidor web.
2. Bloquear acesso direto a configurações, logs, binários e artefatos internos, conforme as necessidades da aplicação.
3. Remover do diretório público arquivos desnecessários à operação.
4. Revisar regras de filtragem de requisições e proteção de diretórios internos.
5. Investigar possível exposição de segredos caso seja comprovada leitura de conteúdo sensível; nesse caso, avaliar revogação e rotação.

Desativar a página de índice não substitui proteger as URLs diretas dos arquivos.

## Critérios de validação após correção

- A URL antes afetada deixa de retornar uma listagem de arquivos.
- Requisições diretas aos artefatos internos recebem bloqueio apropriado, sem conteúdo sensível.
- As funcionalidades públicas necessárias continuam operacionais.
- As evidências de validação distinguem bloqueio, ausência de arquivo, erro de aplicação e redirecionamento para autenticação.

## Tratamento da publicação

Esta nota preserva apenas a descrição técnica, o impacto confirmado, os limites e as recomendações. Nomes de organizações avaliadas, endereços, rotas específicas, datas de coleta, identificadores, capturas e evidências brutas foram omitidos para reduzir a possibilidade de identificação do ambiente.
