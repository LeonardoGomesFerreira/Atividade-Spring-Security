# Atividade Spring Security

Projeto desenvolvido para praticar conceitos básicos de Spring Security em APIs REST utilizando Spring Boot.

---

# Tecnologias utilizadas

- Java 17
- Spring Boot
- Spring Security
- Spring Data JPA
- H2 Database
- Maven
- Lombok

---

# Estrutura do projeto

```text
src/main/java/com/example/atividade_security

├── controller
│   └── ProdutoController.java
│
├── service
│   └── ProdutoService.java
│
├── repository
│   └── ProdutoRepository.java
│
├── entity
│   └── Produto.java
│
├── filters
│   └── SecurityFilter.java
│
└── AtividadeSecurityApplication.java
```

---

# Funcionalidades

- Listar produtos
- Cadastrar produtos
- Configuração básica do Spring Security
- API Stateless
- Rotas públicas e privadas

---

# Configuração de Segurança

A aplicação possui:

- CSRF desabilitado
- SessionCreationPolicy.STATELESS
- Rotas públicas utilizando permitAll()
- Rotas privadas utilizando authenticated()

---

# Classe SecurityFilter

```java
package com.example.atividade_security.filters;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import org.springframework.http.HttpMethod;

import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.http.SessionCreationPolicy;

import org.springframework.security.web.SecurityFilterChain;

@Configuration
public class SecurityFilter {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {

        http
            .csrf(csrf -> csrf.disable())

            .sessionManagement(session ->
                session.sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            )

            .authorizeHttpRequests(auth -> auth

                .requestMatchers(HttpMethod.GET, "/produtos")
                .permitAll()

                .requestMatchers(HttpMethod.POST, "/produtos")
                .permitAll()

                .anyRequest()
                .authenticated()
            );

        return http.build();
    }
}
```

---

# Rotas da API

## Listar produtos

```http
GET /produtos
```

Resposta:

```json
[
  {
    "id": 1,
    "nome": "Notebook",
    "preco": 3500.0
  }
]
```

---

## Cadastrar produto

```http
POST /produtos
```

Body:

```json
{
  "nome": "Mouse Gamer",
  "preco": 150.0
}
```

---

## Rota protegida

```http
GET /produtos/usuarios
```

Resposta esperada:

```text
401 Unauthorized
```

---

# Como executar o projeto

## Clonar repositório

```bash
git clone https://github.com/LeonardoGomesFerreira/Atividade-Spring-Security.git
```

---

## Entrar na pasta

```bash
cd Atividade-Spring-Security
```

---

## Executar projeto

Linux/Mac:

```bash
./mvnw spring-boot:run
```

Windows:

```bash
mvnw.cmd spring-boot:run
```

---

# Testes

Os testes podem ser realizados utilizando:

- Postman
- Insomnia

---

# Objetivo da atividade

Praticar:

- Spring Security
- Segurança em APIs REST
- Configuração Stateless
- Liberação de endpoints
- Proteção de rotas

---

# Autor

Leonardo Gomes Ferreira
