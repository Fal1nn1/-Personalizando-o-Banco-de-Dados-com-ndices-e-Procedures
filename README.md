# -Personalizando-o-Banco-de-Dados-com-ndices-e-Procedures

CREATE PROCEDURE gerenciar_dados(
    -- Variáveis de entrada
    IN _operacao INT,
    IN _identificador INT,
    IN _nome_funcionario VARCHAR(255),
    IN _setor VARCHAR(255),
    IN _salario_funcionario DECIMAL(10,2)
)
BEGIN
    -- Variável de controle
    DECLARE _resultado_operacao VARCHAR(255);

    -- Verifica a operação a ser executada
    CASE _operacao
        WHEN 1 THEN
            -- Consulta
            SELECT * FROM company.funcionarios WHERE id = _identificador;

            SET _resultado_operacao = 'Consulta realizada';
        WHEN 2 THEN
            -- Atualização
            UPDATE company.funcionarios
            SET nome = _nome_funcionario, departamento = _setor, salario = _salario_funcionario
            WHERE id = _identificador;

            SET _resultado_operacao = 'Atualização realizada';
        WHEN 3 THEN
            -- Deleção
            DELETE FROM company.funcionarios WHERE id = _identificador;

            SET _resultado_operacao = 'Deleção realizada';
        ELSE
            SET _resultado_operacao = 'Operação inválida';
    END CASE;

    -- Mensagem de feedback
    SELECT CONCAT('Operação concluída: ', _resultado_operacao);
END //
