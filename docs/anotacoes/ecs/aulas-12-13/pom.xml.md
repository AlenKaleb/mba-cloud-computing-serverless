# ecs/aulas-12-13/pom.xml anotado

## Visão geral
Define o projeto Maven de uma aplicação Spring Boot. Centraliza dependências e plugins, incluindo o BOM da AWS SDK para padronizar versões. É o **contrato de build** da aplicação.

### Conceitos e padrões
- **Maven POM**: descreve metadados, dependências e plugins.
- **Spring Boot Parent**: herda configurações comuns do ecossistema.
- **Dependency Management**: fixa versões via BOM (Bill of Materials).
- **Plugin de empacotamento**: o `spring-boot-maven-plugin` cria jar executável.

## Trechos com anotações
1. **Parent Spring Boot**: garante compatibilidade e versions alignment.
2. **Coordenadas do projeto**: `groupId`, `artifactId`, `version` identificam o artefato.
3. **Java 17**: configura compilação e runtime.
4. **BOM da AWS SDK**: alinha versões dos módulos AWS.
5. **Dependências**: web starter, testes e Lombok (opcional).
6. **Plugin de build**: empacota com exclusão do Lombok no runtime.

## Código completo
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>3.2.5</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>org.acme</groupId>
	<artifactId>java-ecs-spring</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>java-ecs-spring</name>
	<description>Demo project for Spring Boot</description>
	<properties>
		<java.version>17</java.version>
	</properties>
	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>software.amazon.awssdk</groupId>
				<artifactId>bom</artifactId>
				<version>2.25.50</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<dependency>
			<groupId>org.projectlombok</groupId>
			<artifactId>lombok</artifactId>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
				<configuration>
					<excludes>
						<exclude>
							<groupId>org.projectlombok</groupId>
							<artifactId>lombok</artifactId>
						</exclude>
					</excludes>
				</configuration>
			</plugin>
		</plugins>
	</build>

</project>
```
