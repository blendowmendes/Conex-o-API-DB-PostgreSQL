# Conex-o-API-DB-PostgreSQL
Tutorial simples de conexão de uma API com banco de dados PostgreSQL usando Knex

Conexão do banco Postegre com a API-REST usando Knex.js

Autor:  Blendow Mendes

Instalar dependências
	npm instal knex pg

No código configure o knex:
import knex from 'knex';
// Variável onde se localiza suas configurações de conexão.
const config = {
    DB_HOST: 'localhost',
    DB_PORT: porta,
    DB_USER: 'seu_usuario',
    DB_NAME: 'seu_banco',
    DB_PASSWORD: 'sua_senha',
    DB_SSL: false, // defina como true se precisar de SSL
};

Informações de conexão dentro do PostgreSQL - PgAdmin4
Host e Porta:
	Clique com o botão direito no nome do servidor e escolha "Properties".
Na aba "Connection", você encontrará o Host e a Port. A porta padrão do PostgreSQL é 5432.
Nome do Banco de Dados:	
	Expanda a árvore do servidor e localize a pasta "Databases".
Clique na pasta "Databases" para ver todos os bancos de dados disponíveis. O nome que você vê lá é o que você usará como DB_NAME.
Usuário e Senha:
Para ver os usuários, expanda a árvore do servidor até "Login/Group Roles". Você verá uma lista de usuários. O que você precisa para se 	conectar pode ser o seu próprio usuário ou outro que tenha acesso ao banco 	de dados.
Se você não souber a senha de um usuário, precisará redefini-la, pois não é exibida no pgAdmin.
	Redefinir a Senha:
Na janela de propriedades do usuário, vá até a aba Definition (Definição).
Na seção Password (Senha), insira a nova senha no campo Password.
Você também pode marcar a opção Login Role para que o usuário possa se conectar ao banco de dados, caso ainda não esteja marcada.
		Clique em Save (Salvar) para aplicar as alterações.
Verificar as Configurações de SSL (se necessário)
Na aba "Connection" das propriedades do servidor, verifique se há configurações de SSL. Se o SSL estiver habilitado, você precisará configurar seu cliente (Knex, neste caso) para usá-lo.
Juntar as informações:
	const config = {
    		DB_HOST: 'endereco_do_servidor', // Ex: 'localhost' ou IP do servidor
    		DB_PORT: 5432,                   
   	 	DB_USER: 'seu_usuario',           // Nome do usuário do banco de dados
    		DB_NAME: 'seu_banco',             // Nome do banco de dados
    		DB_PASSWORD: 'sua_senha',         // Senha do usuário
    		DB_SSL: false,                    // Defina como true se SSL estiver habilitado
};
Dentro do código:	
const db = knex({
    	client: 'pg',
    	connection: {
        	host: config.DB_HOST,
        	port: config.DB_PORT,
        	user: config.DB_USER,
        	database: config.DB_NAME,
        	password: config.DB_PASSWORD,
        	ssl: config.DB_SSL ? { rejectUnauthorized: false } : false,
    },
});
// Exporta a instância do Knex - o nome db é de escolha do usuário
export default db;
Iniciar Servidor:
// Inicia o servidor - Mude o "PORT" a porta definida 
app.listen(PORT, () => {
    console.log(`Servidor rodando na porta ${PORT}`);
});
	

