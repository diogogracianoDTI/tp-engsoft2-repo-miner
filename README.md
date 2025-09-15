# tp-engsoft2-repo-miner

## Membros do Grupo
- Guilherme Gomes Palhares Gomide
- Diogo Alves Graciano
- Victor Yuji Yano
- Guilherme Novais de Souza

## Explicação do Sistema

A ideia da nossa ferramenta é criar um **utilitário de linha de comando** que ajude a entender o quanto um repositório de software está sendo bem mantido. Muitas vezes um projeto parece ativo, mas olhando de perto dá pra ver sinais de abandono e dependências antigas com possíveis vulnerabilidades conhecidas. Nossa proposta é justamente minerar os repositórios e mostrar esses sinais de forma clara.

O sistema vai olhar para alguns pontos principais:

* **Atividade recente**: frequência e intervalo dos commits, tempo entre releases e merges.
* **Regularidade da manutenção**: períodos longos sem atualização, ritmo de contribuições e engajamento da comunidade.
* **Dependências**: identificar bibliotecas desatualizadas e listar vulnerabilidades já mapeadas nelas.
* **Saúde do repositório**: número de contribuidores ativos, issues acumuladas, pull requests paradas, branches órfãs.

Os resultados poderão ser exportados em formatos como JSON ou CSV e também apresentados em gráficos e indicadores para facilitar a interpretação. No fim, a ferramenta vai funcionar como um “termômetro de manutenção”, dando uma visão geral da saúde de um projeto e ajudando a identificar riscos de obsolescência e segurança.

## Possíveis Tecnologias Utilizadas

Podemos usar ferramentas de mineração como **PyDriller** e **GitPython** para analisar repositórios Git, a **API do GitHub** para complementar com dados de issues e PRs, e bibliotecas como **Typer/Click** para construir a CLI. Na parte de análise de código e dependências, podemos integrar coisas como **tree-sitter**, **Bandit** e scanners de vulnerabilidade como o **OWASP Dependency-Check**.
