O código que você forneceu é um aplicativo JavaFX para um editor de grafos. Para executá-lo no VS Code do zero, você precisará configurar seu ambiente de desenvolvimento para suportar Java e, especificamente, JavaFX.

Aqui está um guia passo a passo completo para fazer isso:

1. Pré-requisitos
Certifique-se de que você tem o seguinte instalado em sua máquina:

Java Development Kit (JDK) 11 ou superior: Você pode verificar sua versão do Java com o comando java -version no terminal. Se não tiver, faça o download e instale o OpenJDK.

Visual Studio Code: Se ainda não o tem, baixe e instale a versão mais recente.

2. Instalar as Extensões Java no VS Code
Abra o VS Code e vá para a seção de extensões (ícone de quatro quadrados no menu lateral ou pressione Ctrl+Shift+X). Instale o pacote de extensões Extension Pack for Java da Microsoft. Ele inclui tudo o que você precisa para desenvolver em Java, como:

Language Support for Java™ by Red Hat

Debugger for Java

Maven for Java

Test Runner for Java

Project Manager for Java

3. Configurar o Projeto JavaFX no VS Code
O JavaFX não está mais incluído no JDK padrão, então você precisará adicioná-lo como uma dependência. A maneira mais fácil de gerenciar isso é usando o Maven.

Passo 3.1: Criar o Projeto Maven
No VS Code, abra a paleta de comandos (Ctrl+Shift+P).

Digite e selecione "Java: Create Java Project".

Selecione "Maven".

Escolha um archetype, como "javafx-archetype-simple". Se você não encontrar essa opção, pode pular essa etapa e criar um projeto Java simples, e depois editar manualmente o arquivo pom.xml.

Insira o groupId (por exemplo, com.example) e o artifactId (por exemplo, editorgrafos).

Escolha um local para salvar o projeto.

Passo 3.2: Configurar o Arquivo pom.xml
Se o archetype não criou o arquivo pom.xml corretamente, ou se você começou com um projeto Java simples, você precisará editar o pom.xml.

O pom.xml deve ter as dependências e o plugin do JavaFX configurados. Cole o seguinte XML no seu arquivo pom.xml, substituindo o conteúdo existente se necessário. Certifique-se de que a versão do JavaFX (17.0.1 no exemplo) corresponda à versão do seu JDK.

--
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>editorgrafos</artifactId>
    <version>1.0-SNAPSHOT</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <javafx.version>17.0.1</javafx.version>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.openjfx</groupId>
            <artifactId>javafx-controls</artifactId>
            <version>${javafx.version}</version>
        </dependency>
        <dependency>
            <groupId>org.openjfx</groupId>
            <artifactId>javafx-fxml</artifactId>
            <version>${javafx.version}</version>
        </dependency>
    </dependencies>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.0</version>
                <configuration>
                    <release>17</release>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.openjfx</groupId>
                <artifactId>javafx-maven-plugin</artifactId>
                <version>0.0.6</version>
                <executions>
                    <execution>
                        <id>default-cli</id>
                        <configuration>
                            <mainClass>com.example.editorgrafos.HelloApplication</mainClass>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
--

Após salvar o arquivo pom.xml, o VS Code deve reconhecer o projeto Maven e começar a baixar as dependências do JavaFX.

4. Adicionar o Código Fonte
Navegue até a pasta src/main/java/com/example/editorgrafos do seu projeto.

Renomeie o arquivo de exemplo, se houver um, para HelloApplication.java ou crie um novo arquivo com esse nome.

Copie e cole todo o código Java que você forneceu no arquivo HelloApplication.java.

5. Executar o Aplicativo
Agora você está pronto para rodar o projeto.

Opção 1: Usando o Terminal
Abra um terminal integrado no VS Code (`Ctrl+``).

Certifique-se de estar no diretório raiz do seu projeto.

Use o comando do Maven para executar a aplicação:

--
mvn clean javafx:run
--

Se tudo estiver configurado corretamente, o JavaFX Maven Plugin irá compilar e executar sua aplicação, e a janela do "Editor de Grafos" deve aparecer.

Opção 2: Usando o Botão de Execução do VS Code
Abra o arquivo HelloApplication.java no editor.

Na parte superior do código, você verá um pequeno ícone de play (triângulo verde) e a palavra "Run" ao lado da declaração da classe HelloApplication.

Clique neste botão "Run".

O VS Code usará as configurações do Maven no pom.xml para executar a aplicação. A janela do "Editor de Grafos" deve abrir.

Se você tiver problemas, verifique se as versões do JDK e do JavaFX no pom.xml são compatíveis e se o caminho para a classe principal (<mainClass>) está correto. O nome do pacote e da classe devem corresponder ao seu arquivo.

Seu aplicativo agora deve estar funcionando, permitindo que você crie e edite grafos.
