# 🎮 Criando um Servidor de Minecraft na AWS (Free Tier)

Este guia mostra como criar e configurar um servidor de **Minecraft Java Edition** utilizando uma instância EC2 na AWS Free Tier.

---

## ☁️ 1. Criando sua conta na AWS

1. Acesse: https://aws.amazon.com/
2. Crie sua conta utilizando o **AWS Free Tier**
3. Após criar a conta, acesse o serviço **EC2**

---

## 🖥️ 2. Criando a Instância EC2

### Configurações utilizadas:

- **Imagem (AMI):** Amazon Linux
- **Tipo de Instância:** `t3.small`  
  > Recomendo uma instância com capacidade maior que `t2.micro` para melhor desempenho.
- **Chave de Segurança (Key Pair):** Crie e baixe sua chave `.pem`
- **Security Group:**  
  - Liberar porta `22` (SSH)
  - Liberar porta `25565` (Minecraft)

Após configurar tudo, clique em **Executar Instância**.

---

## 📥 3. Baixando o Servidor do Minecraft

Acesse o site oficial:

https://www.minecraft.net/en-us/download/server

Baixe a versão desejada do servidor (arquivo `.jar`).

---

## 🔐 4. Acessando sua Instância via SSH

No Windows, abra o **Prompt de Comando**.

Navegue até onde está sua chave `.pem`:

```bash
cd Área de Trabalho
```

Conecte-se via SSH:

```bash
ssh -i sua-chave.pem ec2-user@SEU-ENDERECO-EC2
```

Exemplo:

```bash
ssh -i sua-chave.pem ec2-user@ec2-xx-xxx-xxx-xx.compute.amazonaws.com
```

---

## 📁 5. Criando Pasta do Servidor

Dentro da instância:

```bash
mkdir minecraft-server
cd minecraft-server
```

---

## ☕ 6. Instalando o Java

Instale o Java 21 (Amazon Corretto):

```bash
sudo dnf install java-21-amazon-corretto -y
```

Verifique a versão:

```bash
java -version
```

---

## 📤 7. Enviando o Arquivo .jar para a EC2

Abra um novo Prompt de Comando (no seu computador).

Use o comando `scp` para enviar o arquivo:

```bash
scp -i sua-chave.pem serverMine.jar ec2-user@SEU-ENDERECO-EC2:/home/ec2-user/minecraft-server
```

---

## ▶️ 8. Iniciando o Servidor

Volte ao primeiro terminal (conectado via SSH).

Confirme se o arquivo está na pasta:

```bash
ls
```

Inicie o servidor definindo a memória  
(esse comando está disponível no site oficial do Minecraft para copiar e colar):

```bash
java -Xmx4G -Xms4G -jar minecraft_server.jar nogui
```

Você pode ajustar:

- `-Xms` → memória inicial
- `-Xmx` → memória máxima

---

## 📜 9. Aceitando o EULA

Após a primeira execução, será criado o arquivo `eula.txt`.

Edite o arquivo:

```bash
vi eula.txt
```

Passos:

- Pressione `i` para editar
- Altere `false` para `true`
- Pressione `ESC`
- Digite `:wq` e pressione `Enter`

---

## ⚙️ 10. Configurando o Servidor

Para editar as configurações:

```bash
vi server.properties
```

Aqui você pode alterar:

- Nome do mundo
- Número máximo de jogadores
- Dificuldade
- Modo de jogo
- PvP
- etc.

---

## 🚀 Tecnologias Utilizadas

- AWS EC2
- Amazon Linux
- SSH
- SCP
- Java (Amazon Corretto)
- Minecraft Server (.jar)

---

## 💡 Observações Importantes

- O Free Tier possui limitações de uso.
- A instância deve estar em execução para o servidor funcionar.
- Lembre-se de parar a instância quando não estiver usando para evitar cobranças.
