# Elo — Portal de recrutamento

Portal demonstrativo com experiências conectadas para candidatos e recrutadores. Aplicação estática em português, sem dependências de execução ou etapa de build.

## Funcionalidades

- Vagas com busca por texto e filtros por área, modelo e nível; detalhes, remuneração e prazo de inscrição.
- Currículo com perfil, experiência, formação e habilidades; anexo opcional em PDF de até 1 MB e exportação em texto.
- Candidaturas com apresentação, acompanhamento das etapas e desistência com preservação do histórico.
- Painel do recrutador com indicadores, criação e edição de vagas, rascunhos, publicação e encerramento das inscrições.
- Quadro de processos com filtros, consulta ao currículo enviado e mudanças manuais de etapa.
- Linha do tempo compartilhada: candidatura → triagem → entrevista → proposta → contratação, além de não selecionado ou desistência.

## Regras e consistência

O modelo valida os dados antes de cada gravação. Candidaturas duplicadas, vagas encerradas ou com prazo vencido e currículos incompletos são bloqueados. As etapas avançam ou retornam uma por vez; retornos e recusas exigem motivo. Processos concluídos preservam o histórico.

Cada candidatura guarda uma cópia do currículo usado no envio. Edições posteriores no perfil não alteram candidaturas anteriores, inclusive a referência ao PDF original. O formato, o tamanho e o cabeçalho dos anexos são validados. Valores de remuneração usam centavos inteiros.

Os dados só são substituídos na interface após uma gravação local bem-sucedida. Alterações concorrentes em outra aba bloqueiam novas gravações até recarregar. Falhas de armazenamento preservam os dados anteriores e o formulário em edição.

## Demonstração local

Os perfis Alex Sander (candidato) e Camila Ribeiro (recrutadora), a empresa, as vagas e as demais pessoas são fictícios. O seletor de experiência não é autenticação. As restrições por perfil demonstram regras de aplicação; não constituem controle de acesso de um servidor.

Tudo fica no `localStorage` do navegador, inclusive PDFs. Não há envio real de candidaturas, e-mails, integração com empresas, sincronização entre dispositivos ou seleção automatizada. Para uso real seriam necessários servidor, autenticação, permissões, armazenamento seguro e medidas de privacidade próprias desse contexto. Use apenas dados fictícios na demonstração. Remover os dados do site no navegador reinicia o conteúdo demonstrativo e apaga as alterações locais.

## Executar

Com Node.js instalado:

```sh
node serve.cjs
```

Abra o endereço impresso, `http://127.0.0.1:8794`. No GitHub Pages, publique a branch `main` a partir da raiz (`/`).

## Verificações

```sh
node --check js/model.js
node --check js/app.js
node tests/model.cjs
```

Os testes cobrem perfis, currículos, documentos, permissões de domínio, candidaturas, transições de etapa, datas, remuneração, persistência e integridade dos dados.

## Arquivos

```text
index.html
css/styles.css
js/model.js          # Regras e validações independentes da interface
js/app.js            # Interface e armazenamento local
tests/model.cjs     # Testes do modelo
serve.cjs           # Servidor local sem dependências
```

As fontes DM Sans e Manrope são carregadas do Google Fonts, com alternativas do sistema quando indisponíveis.
