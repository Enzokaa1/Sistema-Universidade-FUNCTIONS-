# Sistema-Universidade-FUNCTIONS-




Relacionamentos:

Um aluno está matriculado em um único curso. (Relacionamento 1 para N entre Alunos e Cursos) Um curso pertence a uma única área. (Relacionamento N para 1 entre Cursos e Áreas)

Diagrama:

+---------------------+ | Alunos | | Cursos | | Áreas |  +---------------------+ | PK: ID | | PK: ID | | PK: ID | | Nome | | Nome | | Nome | | Email | | Descrição | +---------------------+ | FK: Curso_ID | | FK: Área_ID | +---------------------+ 






Entidades:

Áreas:

Atributos: ID (PK), Nome

Cursos:

Atributos: ID (PK), Nome, Descrição, Área_ID (FK)

Alunos:

Atributos: ID (PK), Nome, Email, Curso_ID (FK)
