CREATE DATABASE IF NOT EXISTS universidade;

USE universidade;

CREATE TABLE IF NOT EXISTS areas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100)
);

CREATE TABLE IF NOT EXISTS cursos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100),
    descricao TEXT,
    area_id INT,
    FOREIGN KEY (area_id) REFERENCES areas(id)
);

CREATE TABLE IF NOT EXISTS alunos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100),
    email VARCHAR(100),
    curso_id INT,
    FOREIGN KEY (curso_id) REFERENCES cursos(id)
);

DELIMITER //

CREATE PROCEDURE inserir_curso(
    IN nome_curso VARCHAR(100),
    IN descricao_curso TEXT,
    IN area_id INT
)
BEGIN
    INSERT INTO cursos (nome, descricao, area_id) 
    VALUES (nome_curso, descricao_curso, area_id);
END //

DELIMITER ;

DELIMITER //

CREATE PROCEDURE selecionar_cursos_por_area(
    IN area_nome VARCHAR(100)
)
BEGIN
    SELECT c.nome, c.descricao
    FROM cursos c
    INNER JOIN areas a ON c.area_id = a.id
    WHERE a.nome = area_nome;
END //

DELIMITER ;

CALL inserir_curso('Nome do Curso', 'Descrição do Curso', 1);

CALL selecionar_cursos_por_area('Nome da Área');

DELIMITER //

CREATE PROCEDURE inserir_aluno(
    IN nome_aluno VARCHAR(100),
    IN sobrenome_aluno VARCHAR(100),
    IN curso_id INT
)
BEGIN
    DECLARE email_aluno VARCHAR(200);
    
    -- Gerando o e-mail com base no nome e sobrenome
    SET email_aluno = CONCAT(nome_aluno, '.', sobrenome_aluno, '@dominio.com');
    
    -- Inserindo o aluno na tabela de alunos
    INSERT INTO alunos (nome, email, curso_id) 
    VALUES (nome_aluno, email_aluno, curso_id);
END //

DELIMITER ;

CALL inserir_aluno('Nome', 'Sobrenome', 1);

DELIMITER //

CREATE PROCEDURE inserir_novo_curso(
    IN nome_curso VARCHAR(100),
    IN descricao_curso TEXT,
    IN area_nome VARCHAR(100)
)
BEGIN
    DECLARE area_id INT;
    
    SELECT id INTO area_id FROM areas WHERE nome = area_nome;
    
    IF area_id IS NULL THEN
        INSERT INTO areas (nome) VALUES (area_nome);
        SET area_id = LAST_INSERT_ID();
    END IF;
    
    -- Inserindo o novo curso
    INSERT INTO cursos (nome, descricao, area_id) 
    VALUES (nome_curso, descricao_curso, area_id);
END //

DELIMITER ;

CALL inserir_novo_curso('Nome do Novo Curso', 'Descrição do Novo Curso', 'Nome da Área');

DELIMITER //

CREATE FUNCTION obter_id_curso(
    nome_curso VARCHAR(100),
    nome_area VARCHAR(100)
)
RETURNS INT
BEGIN
    DECLARE curso_id INT;
    
    SELECT c.id INTO curso_id
    FROM cursos c
    INNER JOIN areas a ON c.area_id = a.id
    WHERE c.nome = nome_curso AND a.nome = nome_area;
    
    RETURN curso_id;
END //

DELIMITER ;

SELECT obter_id_curso('Nome do Curso', 'Nome da Área');

DELIMITER //

CREATE PROCEDURE matricular_aluno(
    IN nome_aluno VARCHAR(100),
    IN email_aluno VARCHAR(100),
    IN nome_curso VARCHAR(100),
    IN nome_area VARCHAR(100)
)
BEGIN
    DECLARE curso_id INT;
    DECLARE aluno_id INT;
    
    SELECT c.id INTO curso_id
    FROM cursos c
    INNER JOIN areas a ON c.area_id = a.id
    WHERE c.nome = nome_curso AND a.nome = nome_area;
    
    SELECT id INTO aluno_id
    FROM alunos
    WHERE nome = nome_aluno AND email = email_aluno;
    
    IF aluno_id IS NULL THEN
        INSERT INTO alunos (nome, email, curso_id) 
        VALUES (nome_aluno, email_aluno, curso_id);
    ELSE
    
        UPDATE alunos
        SET curso_id = curso_id
        WHERE id = aluno_id;
    END IF;
END //

DELIMITER ;

CALL matricular_aluno('Nome do Aluno', 'email@dominio.com', 'Nome do Curso', 'Nome da Área');

DELIMITER //

CREATE PROCEDURE matricular_aluno(
    IN nome_aluno VARCHAR(100),
    IN email_aluno VARCHAR(100),
    IN nome_curso VARCHAR(100),
    IN nome_area VARCHAR(100)
)
BEGIN
    DECLARE curso_id INT;
    DECLARE aluno_id INT;
    
    SELECT c.id INTO curso_id
    FROM cursos c
    INNER JOIN areas a ON c.area_id = a.id
    WHERE c.nome = nome_curso AND a.nome = nome_area;
    
    SELECT id INTO aluno_id
    FROM alunos
    WHERE nome = nome_aluno AND email = email_aluno;
    
    IF aluno_id IS NULL THEN
        INSERT INTO alunos (nome, email, curso_id) 
        VALUES (nome_aluno, email_aluno, curso_id);
    ELSE

        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'O aluno já está matriculado em um curso.';
    END IF;
END //

DELIMITER ;

INSERT INTO alunos (nome, email, curso_id) VALUES
('Lucas Almeida', 'lucas.almeida@dominio.com', 1),
('Ana Pereira', 'ana.pereira@dominio.com', 3),
('Marcela Vieira', 'marcela.vieira@dominio.com', 2),
('César Lima', 'cesar.lima@dominio.com', 3),
('Rafaela Almeida', 'rafaela.almeida@dominio.com', 1),
('Márcia Oliveira', 'marcia.oliveira@dominio.com', 3),
('João Silva', 'joao.silva@dominio.com', 2),
('Débora Pereira', 'debora.pereira@dominio.com', 1),
('Viviane Lima', 'viviane.lima@dominio.com', 2),
('Daniel Santos', 'daniel.santos@dominio.com', 1),
('Mariana Lima', 'mariana.lima@dominio.com', 3),
('Juliana Souza', 'juliana.souza@dominio.com', 2),
('Patrícia Santos', 'patricia.santos@dominio.com', 1),
('Elaine Souza', 'elaine.souza@dominio.com', 3),
('Maria Santos', 'maria.santos@dominio.com', 2),
('Pedro Oliveira', 'pedro.oliveira@dominio.com', 1),
('Vanessa Ferreira', 'vanessa.ferreira@dominio.com', 2),
('Rafael Ferreira', 'rafael.ferreira@dominio.com', 3),
('Rodrigo Martins', 'rodrigo.martins@dominio.com', 1),
('Jéssica Lima', 'jessica.lima@dominio.com', 3),
('Sandra Costa', 'sandra.costa@dominio.com', 1),
('Marcelo Vieira', 'marcelo.vieira@dominio.com', 3),
('Gabriel Santos', 'gabriel.santos@dominio.com', 2),
('Helena Vieira', 'helena.vieira@dominio.com', 1),
('Vivian Martins', 'vivian.martins@dominio.com', 2),
('Bruno Vieira', 'bruno.vieira@dominio.com', 3),
('Felipe Santos', 'felipe.santos@dominio.com', 1),
('Guilherme Costa', 'guilherme.costa@dominio.com', 2),
('André Costa', 'andre.costa@dominio.com', 3),
('Thiago Pereira', 'thiago.pereira@dominio.com', 2),
('Leandro Oliveira', 'leandro.oliveira@dominio.com', 3),
('Isabela Santos', 'isabela.santos@dominio.com', 1),
('Aline Gonçalves', 'aline.goncalves@dominio.com', 2),
('Juliana Almeida', 'juliana.almeida@dominio.com', 3),
('Renata Santos', 'renata.santos@dominio.com', 1),
('Camila Costa', 'camila.costa@dominio.com', 2),
('Mateus Martins', 'mateus.martins@dominio.com', 3),
('Paulo Gonçalves', 'paulo.goncalves@dominio.com', 1),
('Tatiane Almeida', 'tatiane.almeida@dominio.com', 2),
('Amanda Souza', 'amanda.souza@dominio.com', 3),
('Cristiano Ferreira', 'cristiano.ferreira@dominio.com', 1),
('Ricardo Vieira', 'ricardo.vieira@dominio.com', 2),
('Marcelo Almeida', 'marcelo.almeida@dominio.com', 3),
('Robson Ferreira', 'robson.ferreira@dominio.com', 1),
('Fernanda Martins', 'fernanda.martins@dominio.com', 2),
('Caroline Gonçalves', 'caroline.goncalves@dominio.com', 3),
('Carla Almeida', 'carla.almeida@dominio.com', 1),
('Lucas Vieira', 'lucas.vieira@dominio.com', 2),
('Marcos Souza', 'marcos.souza@dominio.com', 3),
('Ana Paula Martins', 'ana.paula.martins@dominio.com', 1),
('Ronaldo Souza', 'ronaldo.souza@dominio.com', 2),
('Roberto Souza', 'roberto.souza@dominio.com', 3),
('Carolina Vieira', 'carolina.vieira@dominio.com', 1),
('Alexandre Oliveira', 'alexandre.oliveira@dominio.com', 2),
('Fábio Gonçalves', 'fabio.goncalves@dominio.com', 3),
('Patrícia Oliveira', 'patricia.oliveira@dominio.com', 1),
('Larissa Gonçalves', 'larissa.goncalves@dominio.com', 2),
('Isabela Gonçalves', 'isabela.goncalves@dominio.com', 3),
('José Martins', 'jose.martins@dominio.com', 1),
('Marcos Vieira', 'marcos.vieira@dominio.com', 2),
('Marcela Santos', 'marcela.santos@dominio.com', 3),
('Rafael Almeida', 'rafael.almeida@dominio.com', 1),
('Débora Lima', 'debora.lima@dominio.com', 2),
('Vivian Souza', 'vivian.souza@dominio.com', 3),
('Mariana Vieira', 'mariana.vieira@dominio.com', 1),
('Daniel Ferreira', 'daniel.ferreira@dominio.com', 2),
('Cristiano Gonçalves', 'cristiano.goncalves@dominio.com', 3),
('Lucas Martins', 'lucas.martins@dominio.com', 1),
('Elaine Pereira', 'elaine.pereira@dominio.com', 2),
('Marcelo Gonçalves', 'marcelo.goncalves@dominio.com', 3),
('Juliana Costa', 'juliana.costa@dominio.com', 1),
('Eduardo Oliveira', 'eduardo.oliveira@dominio.com', 2),
('Beatriz Pereira', 'beatriz.pereira@dominio.com', 3),
('Rodrigo Souza', 'rodrigo.souza@dominio.com', 1),
('Vanessa Santos', 'vanessa.santos@dominio.com', 2),
('Leandro Costa', 'leandro.costa@dominio.com', 3),
('Fernanda Almeida', 'fernanda.almeida@dominio.com', 1),
('Guilherme Martins', 'guilherme.martins@dominio.com', 2),
('César Vieira', 'cesar.vieira@dominio.com', 3),
('Larissa Souza', 'larissa.souza@dominio.com', 1),
('Lucas Costa', 'lucas.costa@dominio.com', 2),
('Gabriela Ferreira', 'gabriela.ferreira@dominio.com', 3),
('Anderson Martins', 'anderson.martins@dominio.com', 1),
('Vivian Oliveira', 'vivian.oliveira@dominio.com', 2),
('Ronaldo Ferreira', 'ronaldo.ferreira@dominio.com', 3),
('Carla Pereira', 'carla.pereira@dominio.com', 1),
('Tatiane Vieira', 'tatiane.vieira@dominio.com', 2),
('Ana Gonçalves', 'ana.goncalves@dominio.com', 3),
('Roberto Costa', 'roberto.costa@dominio.com', 1),
('Juliana Lima', 'juliana.lima@dominio.com', 2),
('Gabriel Almeida', 'gabriel.almeida@dominio.com', 3),
('Camila Vieira', 'camila.vieira@dominio.com', 1),
('Paulo Souza', 'paulo.souza@dominio.com', 2),
('Sandra Pereira', 'sandra.pereira@dominio.com', 3),
('Alexandre Costa', 'alexandre.costa@dominio.com', 1),
('Júlia Martins', 'julia.martins@dominio.com', 2),
('Daniel Vieira', 'daniel.vieira@dominio.com', 3);


INSERT INTO cursos (nome, descricao, area_id) VALUES
('Engenharia de Software', 'Curso de Engenharia de Software', 1),
('Astrofísica', 'Curso de Astrofísica', 2),
('Sociologia', 'Curso de Sociologia', 3),
('Gastronomia', 'Curso de Gastronomia', 4),
('Ciências Ambientais', 'Curso de Ciências Ambientais', 5),
('Filosofia', 'Curso de Filosofia', 6),
('Teatro', 'Curso de Teatro', 7),
('Publicidade e Propaganda', 'Curso de Publicidade e Propaganda', 8),
('Antropologia', 'Curso de Antropologia', 9),
('Biomedicina', 'Curso de Biomedicina', 10),
('Engenharia Mecânica', 'Curso de Engenharia Mecânica', 11),
('Relações Internacionais', 'Curso de Relações Internacionais', 12),
('Zoologia', 'Curso de Zoologia', 13),
('Ciência Política', 'Curso de Ciência Política', 14),
('Engenharia Química', 'Curso de Engenharia Química', 15),
('Serviço Social', 'Curso de Serviço Social', 16),
('Turismo', 'Curso de Turismo', 17),
('Design de Interiores', 'Curso de Design de Interiores', 18),
('Ciências Atuariais', 'Curso de Ciências Atuariais', 19),
('Cinema', 'Curso de Cinema', 20),
('Biblioteconomia', 'Curso de Biblioteconomia', 21),
('Geologia', 'Curso de Geologia', 22),
('Fisioterapia', 'Curso de Fisioterapia', 23),
('Meteorologia', 'Curso de Meteorologia', 24),
('Odontologia', 'Curso de Odontologia', 25);
