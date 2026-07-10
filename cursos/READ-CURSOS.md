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
•
Adicionar uma nova categoria (ex: "Bolsas"): Só adicionar o bloco no JSON. O app cria o botão sozinho.
•
Adicionar um curso novo: Criar o JSON no GitHub e registrar o nome dele no CourseViewModel.kt.
