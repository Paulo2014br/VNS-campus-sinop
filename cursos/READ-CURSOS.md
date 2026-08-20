Passo 1: Criar o arquivo JSON do curso
Para cada curso que você quiser adicionar, crie um arquivo novo no seu repositório do GitHub dentro da pasta cursos/.
1.
O nome do arquivo deve ser exatamente o ID que você usará no código (ex: agronomia.json).
2.
Use este modelo (template) para preencher:

{
  "id": "agronomia",
  "nome": "Agronomia - Bacharelado",
  "tem_conteudo": true,
  "categorias": [
    {
      "nome": "Ligas Acadêmicas",
      "itens": [
        {
          "id": "liga_exemplo",
          "titulo": "Nome da Liga",
          "subtitulo": "Subtítulo Opcional",
          "descricao": "Texto completo que aparece no BottomSheet.",
          "instagram_url": "https://instagram.com/perfil"
        }
      ]
    },
    {
      "nome": "Projetos de Extensão",
      "itens": []
    }
  ]
}

Passo 2: Registrar o curso no aplicativo
Atualmente, a "lista mestre" de cursos está no código. Para que o app saiba que o novo curso existe, você precisa adicioná-lo no arquivo CourseViewModel.kt:
1.
Abra o arquivo CourseViewModel.kt.
2.
Vá até a função carregarListaPrincipal().
3.
Adicione o novo curso à lista:
Kotlin
_listaCursos.value = listOf(
    CursoData("medicina_veterinaria", "Medicina Veterinária - Bacharelado", true),
    CursoData("agronomia", "Agronomia - Bacharelado", true), // <-- Adicione assim
    CursoData("enfermagem", "Enfermagem - Bacharelado", true) // O terceiro parâmetro 'true' ativa o download
)
Passo 3: Conferir o Link no GitHub (Importante)
Certifique-se de que a estrutura no seu repositório VNS-campus-sinop seja esta:
•
main/ (branch principal)
◦
cursos/ (pasta)
▪
medicina_veterinaria.json
▪
agronomia.json
▪
enfermagem.json
[!TIP] Dica de Ouro: Se você quiser que as imagens (logos das ligas) também sejam dinâmicas, suba as imagens em uma pasta assets/ no GitHub e coloque o link direto delas no campo "imagem_url" do seu JSON.
Resumo de Manutenção
•
Mudar texto ou link de Instagram: Só editar o JSON no GitHub. O app atualiza na hora!


. O Repositório GitHub (VNS-campus-sinop)
Você usa o GitHub como seu servidor de dados. A pasta principal é a cursos/ e o link base que o app acessa é o raw.githubusercontent.com.
•
lista_cursos.json: É o "índice" do app. Ele contém uma lista simples com o nome de cada curso e o id (que deve ser o nome do arquivo JSON detalhado).
•
{id}.json (ex: medicina_veterinaria.json): Contém o conteúdo pesado. Aqui você definiu as Categorias (Projetos de Extensão, Ligas Acadêmicas, etc.) e os Itens dentro de cada categoria.
2. Modelagem de Dados (  CourseModels.kt)
Você criou classes que espelham exatamente o seu JSON:
•
CursoData: Representa o curso e sua lista de categorias.
•
CategoriaData: Agrupa os itens (ex: uma lista só de Ligas).
•
ItemConteudoData: Contém o título, subtítulo, link do Instagram e a descrição detalhada.
3. Lógica do App (  CourseViewModel.kt)
A ViewModel faz o "trabalho sujo" de buscar os dados:
•
OkHttpClient + Gson: O app faz uma requisição HTTP para o GitHub, baixa o texto do JSON e o transforma em objetos Kotlin automaticamente.
•
Carregamento Sob Demanda: Ao abrir a tela, ele baixa a lista de cursos. Só quando o usuário clica em um curso específico é que o app baixa o arquivo JSON detalhado daquele curso (economizando dados).
4. Interface e Navegação (  CourseContentActivity.kt)
Toda a tela foi feita em Jetpack Compose, organizada em estados:
•
Fluxo de Telas: Lista de Cursos -> Categorias -> Itens da Categoria.
•
Botão Voltar: A TopAppBar muda o título e a ação do botão conforme o nível de profundidade que o usuário está.
•
Intersticial: O app está configurado para mostrar um anúncio Intersticial logo na entrada da tela e depois a cada 10 cliques (conforme a função deveMostrarInterstitial).
•
Conteúdo Bloqueado (Rewarded): Você implementou uma trava de segurança. A descrição completa e o botão do Instagram só aparecem se o usuário assistir a um vídeo de recompensa (Anúncio Premiado), acionando a função liberarConteudo().
Como adicionar novos conteúdos agora?
1.
Crie o arquivo JSON do curso no GitHub (ex: enfermagem.json) seguindo o template que você deixou no READ-CURSOS.md.
2.
Adicione o novo curso (id e nome) no arquivo lista_cursos.json no GitHub.
3.
O app irá carregar o novo curso automaticamente na próxima vez que for aberto!
Você não precisa mexer em nada no código do Android Studio para adicionar novos cursos, apenas editar os arquivos no GitHub.
•
Adicionar uma nova categoria (ex: "Bolsas"): Só adicionar o bloco no JSON. O app cria o botão sozinho.
•
Adicionar um curso novo: Criar o JSON no GitHub e registrar o nome dele no CourseViewModel.kt.
